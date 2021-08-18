+++
title = "5CTA0 - Statistical signal processing"

# date = {{ .Date }}
lastmod = 2021-08-17

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "s.turco@tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "5CTA0 - Statistical Signal Processing"
weight = 1

+++

<!-- ## News
<ul>
<li> 17/09/2020: From today, we will have an extra Q&A session each Thursday at 13.30. Moreover, the sessions are planned for 90 minutes instead of 45. We will end them earlier if there are no more things to discuss. Please check the updated schedule below</a>.  </li>

<li> 20/08/2020: Due to the COVID-19 situation, the 2020-21 edition of the course will be given fully online. If the situation allows, on campus instructions will be planned on the second half of the course.  </li>

<li> 19/08/2020: To ease communications, we have created a <i>Discord</i> channel. You are welcome to join <a href=https://discord.gg/fRVNXuK >here</a>. All official communications, however, will be always given on <a href=https://canvas.tue.nl/courses/15713>Canvas</a>.  </li>
</ul> -->

## Introduction

As variability and noise affect all measurements, all signals are inherently a stochastic variable. Deterministic approaches to signal  processing are thus inadequate for many real-world applications. Be it a radar signal to detect a airplane, an electrocardiogram to diagnose hearth conditions, or a GPS signal to guide an autonomous car, virtually every engineer deals with real-world signals, affected by several sources of noise and interference. Understanding how to handle and process signals in the presence of uncertainty, e.g., “random” signals, is thus fundamental for every student aiming at becoming an engineer. This course provides the basic tools necessary for accurate and reliable processing of random signals.

The course is divided in three modules and it includes a blend of reading and video materials, quizzes, and assignments. The first module cover topics of probability, random variables and random processes and is a pre-requisite for the following modules. The second modules dives into estimation theory and estimation methods including least-square, maximum likelihood and Bayesian estimation; the application of estimation  theory in the context of spectral analysis is also discussed. The final module covers hypothesis testing and detection theory, with applications for detecting a deterministic signal in noise.

## Learning goals

At the end of the course, you will be able to:

<ul>
<li>Understand the basic principles of probability including probability axioms, independence, conditional probability, Bayes theorem and use these principles in solving problems.  </li>

<li>Explain the difference between deterministic and stochastic signals providing examples in the context of signal processing.  </li>

<li>Understand and reflect on the implications of the central limit theorem in the context of signal acquisition and analysis.  </li>

<li>Characterize random variables using probability distributions, expected value, variance, and moments.  </li>

<li>Characterize random signals by computing first and second order statistics.  </li>

<li>Calculate the Cramer-Rao lower bound for the variance of an estimator, given the noise statistics.  </li>

<li>Calculate the bias and variance of an estimator, given the noise statistics.  </li>

<li>Apply the least squares, maximum likelihood and Bayesian estimations methods to solve problems concerning the estimation of signal model parameters.  </li>

<li>Decide which estimation method to use to solve an estimation problem based on the signal model and availability of noise statistics.  </li>

<li>Apply numerical solution methods to obtain the least squares and maximum likelihood estimates for problems with nonlinear signal models.  </li>

<li>Calculate the threshold to achieve a desired false alarm probability and the resulting detection probability based on Neyman-Pearson theorem when given signal statistics for two different hypotheses. </li>

<li>Plot receiver operating characteristic curves to show the performance of a Neyman-Pearson detector, given signal statistics for two different hypotheses. </li>

<li>Explain how the Student’s t test is applied to hypothesis testing.</li>
</ul>

<br></br>

## Study material

The available material consists of:

<ul>
  <li> <b>Reading material</b> - This includes all study material for the course and is available under the below specified modules on this platform. </li>
  <li> <b>Screencast videos</b> - Besides the extensive reading material, short informative videos are provided to explain the subject material. </li>
  <li> <b>Quizzes</b> - Short quizzes to test whether you have fully understood the subject matter as explained in the screencast videos. </li>
  <li> <b>Exercises</b> - Homework exercises to help you fully understand the subject matter. Some exercises are mandatory for the tutorial sessions. </li>
  <li> <b>Pencast videos</b> - Of some homework exercises, pencast videos are available that walk through the entire exercise. </li>
  <li> <b>MATLAB labs</b> - Mandatory labs are available to apply the learned material using MATLAB. </li>
  <li> <b>MATLAB demos</b> - Matlab live scripts to put theoretical knowledge into practice and further enhance your learning experience</li>
</ul>
For the final examination only knowledge of the reading material and a good understanding of the homework exercises is required. However, all the other material will complement the learning process significantly.

### Additional reading material
The material covered in this course is based on:

<ul>
  <li> Steven M. Kay, "Fundamentals of Statistical Signal Processing, Volume I - Estimation Theory" . </li>
  <li> Steven M. Kay, "Fundamentals of Statistical Signal Processing, Volume II - Detection Theory"  </li>
  <li> Dimitris G. Manolakis et al. "Statistical and adaptive signal processing"</li>
  <li> Peter M. Clarkson, "Optimal and Adaptive Signal Processing" </li>
  <li>  Silvia Maria Alessio, "Digital Signal Processing and Spectral Analysis for Scientists - Concepts and Applications" </li>
</ul>

We also suggest the following websites:

<ul>
<li><a href=https://seeing-theory.brown.edu/#firstPage >Seeing theory by Brwon University</a> </li>
</ul>

<br></br>

## Planning

A detailed planning for tha academic year 2021-22 is available on Canvas <a href=https://canvas.tue.nl/courses/15713/assignments/syllabus >Canvas.</a>



<!-- | Week   |         Lectures         |                        Instruction/Labs                         | Topics                                                                   |                                     |
|:------:|:-----------------------:|:---------------------------------------------------------------:|--------------------------------------------------------------------------|-----------------------------------------------|
|   1    | 31/08/2020<br>08.45-9.30  |         No instructions<br><p style="color:#4E5480">Labs 03/09/2020<br>15.30 - 17.20</p>         | 1.1 Probability and random variables                                   | Quiz Week 1<br>Survey Week 1<br>MATLAB Demo 1  |
|   2    | 07/09/2020<br>08.45-9.30  | Inst 07/09/2020<br>10.45 - 12.35<br> <p style="color:#4E5480">Labs 10/09/2020<br>15.30 - 17.20</p>   | 1.2 Random processes and random signals<br>1.3 Rational signal models     | Quiz Week 2<br>Survey Week 2<br>MATLAB Demo 2   |
|   3    | 14/09/2020<br>08.45-9.30<br><p style="color:#4E5480">17/09/2020<br>13.30-14.30</p>   | Inst 14/09/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 17/09/2020<br>15.30 - 17.20</p>   | 2.1 Least square estimation<br>2.2 Maximum Likelihood Estimation           | Quiz Week 3<br>Survey Week 3<br>MATLAB Demo 3  |
|   4    | 21/09/2020<br>08.45-10.15<br><p style="color:#4E5480">24/09/2020<br>13.30-14.30</p>   | Inst 21/09/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 24/09/2020<br>15.30 - 17.20</p>   | 2.3 Bias, Variance, Cramer-Rao Lower Bound<br>2.4 MVUE for Linear models  | Quiz Week 4<br>Survey Week 4<br>MATLAB Demo 4  |
|   5    | 28/09/2020<br>08.45-10.15<br><p style="color:#4E5480">01/10/2020<br>13.30-14.30</p>   | Inst 28/09/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 01/10/2020<br>15.30 - 17.20</p>   | 2.5 Bayesian estimator<br>2.6 Numerical estimation methods                 | Quiz Week 5<br>Survey Week 5<br>MATLAB Demo 5   |
|   6    | 05/10/2020<br>08.45-10.15<br><p style="color:#4E5480">08/10/2020<br>13.30-14.30</p>   | Inst 05/10/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 08/10/2020<br>15.30 - 17.20</p>   | 2.7 Spectral estimation                                                  | Quiz Week 6<br>Survey Week 6<br>MATLAB Demo 6   |
|   7    | 12/10/2020<br>08.45-10.15<br><p style="color:#4E5480">15/10/2020<br>13.30-14.30</p>   | Inst 12/10/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 15/10/2020<br>15.30 - 17.20</p>   | 3.1 Hypothesis testing<br>3.2 Matched filter                               | Quiz Week 7<br>Survey Week 7<br>MATLAB Demo 7   |
|   8    | 19/10/2020<br>08.45-10.15<br><p style="color:#4E5480">22/10/2020<br>13.30-14.30</p>   | Inst 19/10/2020<br>10.45 - 12.35<br><p style="color:#4E5480">Labs 22/10/2020<br>15.30 - 17.20</p>   | 3.3 Statistical tests<br>Old exams review                                  | Quiz Week 8<br>Survey Week 8<br>MATLAB Demo 8   | -->

## Contact
In case any of the above material is unclear, please contact the responsible teachers of this course, dr. S. Turco (s.turco@tue.nl) and ir. F. Lampel (f.lampel@tue.nl). If there are any problems with the platform or with the material on the platform, please put the mail address sps.education@tue.nl in the CC of your email, or simply click <a href="mailto:{{< param responsibleteacher >}}?cc=sps.education@tue.nl&subject=[5CTA0]%20platform:%20{specify problem here}">here</a>. This will help us keep the platform up-to-date.
