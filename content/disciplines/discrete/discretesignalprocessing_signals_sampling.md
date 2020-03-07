+++
title = "Sampling process"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling process"
  weight = 1
  parent = "Discrete-time signals"


+++

As discussed in the previous module about sampling, the conversion of an analog or continuous-time signal $x(t)$ to the digital domain
is carried out by a C-to-D convertor as indicated in the figure below.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/asignal.svg"
      alt="C-to-D conversion."
    />
    <figcaption>
      C-to-D conversion.
    </figcaption>
  </figure>
</div>

The convertor runs at a sampling rate of $f_s=1/T_s$ [samples/second], in which $T_s$ is the inter-sample distance.
In the discrete domain the signals are represented as sequences of numbers called samples. A sample value of a typical discrete-time signal or sequence is denoted as $x[n \cdot T_s]$. Square brackets are used to denote the difference with continuous-time signals.
Furthermore, in most cases the notation $T_s$ is skipped and the samples are denoted by $x[n]$. Although the independent variable $n$ need not necessarily represent 'time', $n$ may for example correspond to a spatial coordinate or distance, $x[n]$ is generally referred to as a function of time with the argument $n$ being an integer in the range $-\infty$ and $+ \infty$. It should be noted that $x[n]$ is defined only for integer values of index $n$ and is undefined for non-integer values of index $n$.  Usually a real-valued signal $x[n]$ is represented in a graph, from which the correspondence with the underlying continuous-time signal becomes clear in case the sampling rate $f_s$ meets the Nyquist criterion.
