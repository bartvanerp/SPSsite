+++
title = "Complex numbers and phasors"

# date = {{ .Date }}
lastmod = 2019-04-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.curriculum]
  name = "Complex numbers and phasors"
  weight = 3

+++

## Introduction
The signal processing field requires a mathematical maturity for a complete understanding of all its topics.
In this section two important concepts will be covered: complex numbers and phasors. A good understanding of these concepts is required to continue with most of the other sections.


### Conceptual videos
The following conceptual video gives a brief overview of the complex numbers and phasors. This video should give a general understanding of these concepts and should prepare you for the slides and the reader.

<div>
<video width="100px" controls>
  <source src="https://github.com/bartvanerp/SPScontent/raw/master/5.%20Introduction%20videos/Introduction%20-%20Complex%20Numbers.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>

\
\
## Information
The theoretical background of this module will be covered by means of a slide deck, which includes the most important aspects of this module, and the reader, which covers the material in more detail.

### Slides
<!---
<object data="https://github.com/bartvanerp/SPScontent/raw/master/1.%20Lecture%20Slides/1.%20CNAP%20-%20Slides.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="https://github.com/bartvanerp/SPScontent/raw/master/1.%20Lecture%20Slides/1.%20CNAP%20-%20Slides.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="https://github.com/bartvanerp/SPScontent/raw/master/1.%20Lecture%20Slides/1.%20CNAP%20-%20Slides.pdf">Download PDF</a>.</p>
    </embed>
</object> -->




<embed src="https://drive.google.com/viewerng/
viewer?embedded=true&url=https://github.com/bartvanerp/SPScontent/raw/master/1.%20Lecture%20Slides/1.%20CNAP%20-%20Slides.pdf" width="100%" height="400px">


### Reader
<!--
<object data="https://github.com/bartvanerp/SPScontent/raw/master/2.%20Readers/1.%20CNaP%20-%20Reader.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="https://github.com/bartvanerp/SPScontent/raw/master/2.%20Readers/1.%20CNaP%20-%20Reader.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="https://github.com/bartvanerp/SPScontent/raw/master/2.%20Readers/1.%20CNaP%20-%20Reader.pdf">Download PDF</a>.</p>
    </embed>
</object> -->

<embed src="https://drive.google.com/viewerng/
viewer?embedded=true&url=https://github.com/bartvanerp/SPScontent/raw/master/2.%20Readers/1.%20CNaP%20-%20Reader.pdf" width="100%" height="400px">


\
\
## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.


### Exercise bundle
<!-- <object data="https://github.com/bartvanerp/SPScontent/raw/master/3.%20Exercises/1.%20CNAP%20-%20Student%20Exercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="https://github.com/bartvanerp/SPScontent/raw/master/3.%20Exercises/1.%20CNAP%20-%20Student%20Exercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="https://github.com/bartvanerp/SPScontent/raw/master/3.%20Exercises/1.%20CNAP%20-%20Student%20Exercises.pdf">Download PDF</a>.</p>
    </embed>
</object> -->

<embed src="https://drive.google.com/viewerng/
viewer?embedded=true&url=https://github.com/bartvanerp/SPScontent/raw/master/3.%20Exercises/1.%20CNAP%20-%20Student%20Exercises.pdf" width="100%" height="400px">

### Answers
Download the answers <a href="https://github.com/bartvanerp/SPScontent/raw/master/3.%20Exercises/Answers/1.%20CNaP%20-%20Student%20Answers.pdf">here</a>.

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
   <source src="https://github.com/bartvanerp/SPScontent/raw/master/6.%20Screencasts/CNAP%20-%202a/CNAP%20-%202a.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-2">
 <video width="500" height="240" controls>
   <source src="https://github.com/bartvanerp/SPScontent/raw/master/6.%20Screencasts/CNAP%20-%205c/CNAP%20-%205c.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-3">
 <video width="500" height="240" controls>
   <source src="https://github.com/bartvanerp/SPScontent/raw/master/6.%20Screencasts/CNAP%20-%206c/CNAP%20-%206c.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-4">
 <video width="500" height="240" controls>
   <source src="https://github.com/bartvanerp/SPScontent/raw/master/6.%20Screencasts/CNAP%20-%208b/CNAP%20-%208b.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-5">
 <video width="500" height="240" controls>
   <source src="https://github.com/bartvanerp/SPScontent/raw/master/6.%20Screencasts/CNAP%20-%2011/CNAP%20-%2011.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

</div>
