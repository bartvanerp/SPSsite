+++
title = "Sampling and aliasing"

# date = {{ .Date }}
lastmod = 2019-04-19

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.curriculum]
  name = "Sampling and aliasing"
  weight = 5

+++

## Introduction
The signal processing field often deals with discretely sampled digital signals for practicality and not with continuous signals. It is important to understand the consequences of this conversion from the continuous to discrete time domain.
In this section two important concepts will be covered: sampling and aliasing. A good understanding of these concepts is required to continue with most of the other sections.


### Conceptual videos
The following conceptual video gives a brief overview of the sampling operation. This video should give a general understanding of the main concept and should prepare you for the slides and the reader.
<configuration>

<div>
<video controls preload>
  <source src="/../files/5.Introduction/Introduction-Aliasing.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>

\
\
## Information
The theoretical background of this module will be covered by means of a slide deck, which includes the most important aspects of this module, and the reader, which covers the material in more detail.

### Slides

<object data="/../files/1.Slides/3.SAA-Slides.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/1.Slides/3.SAA-Slides.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/1.Slides/3.SAA-Slides.pdf">Download PDF</a>.</p>
    </embed>
</object>


### Reader

<object data="/../files/2.Reader/3.SAA-Reader.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/2.Reader/3.SAA-Reader.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/2.Reader/3.SAA-Reader.pdf">Download PDF</a>.</p>
    </embed>
</object>

\
\
## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


### Exercise bundle

<object data="/../files/3.Exercises/3.SAA-StudentExercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/3.SAA-StudentExercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/3.SAA-StudentExercises.pdf">Download PDF</a>.</p>
    </embed>
</object>

### Answers
Download the answers <a href="/../files/3.Exercises/Answers/3.SAA-StudentAnswers.pdf">here</a>.

### Pencast videos
<script src='https://vjs.zencdn.net/7.4.1/video.js'></script>
<div class="grid-row reverse video-gallery">
 <input type="radio" value="1" name="video-list" id="video-1" checked="checked" /><label for="video-1">Exercise 1</label>
 <input type="radio" value="2" name="video-list" id="video-2" /><label for="video-2">Exercise 7</label>
 <input type="radio" value="3" name="video-list" id="video-3" /><label for="video-3">Exercise 12</label>


 <!-- videos -->
 <div class="video video-1">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SAA-1.mp4" type="video/mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-2">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SAA-7.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-3">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SAA-12.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

</div>
