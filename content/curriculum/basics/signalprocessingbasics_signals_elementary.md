+++
title = "Elementary signals and notation"

# date = {{ .Date }}
lastmod = 2019-06-03

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.basics]
  name = "Elementary signals and notation"
  parent = "Basic signals"
  weight = 2.3

+++
Before turning to difficult signal processing problems, it is important to know how to describe a signal.
Furthermore it is beneficial to know some basic signal that are commonly used in examples.


## Signal notation
When processing signals it is important to know how these signals can be denoted formally.
There are two classes of signals.
One of them is a continuous-time signal and the other one is a discrete-time signal.

The continuous signal is usually denoted as $x(t)$, where $x$ denotes the identifier of the signal and $t$ denotes the continuous-time domain.
The round brackets $(\cdot)$ denote that we are dealing with a continuous-time signal.
This means that the signal can be evaluated at any moment in time.

The second class of signals is the discrete-time signal and is denoted by $x[n]$, where again $x$ is the signal identifier and $n$ denotes the sample index.
The square brackets $[\cdot]$ denote that we are now dealing with a discrete-time signal.
The difference between the continuous-time signal is that the signal can now only be evaluated at discrete moments in time denoted by $n$.
The signal now consist out of many points of data, where each point can be accessed by its index.
Computers are unable to process continuous signals, because of the discrete memory, and therefore can only process discrete-time signals.
The process where a continuous-time signal is converted to a discrete-time signal and back is described <a href="../signalprocessingbasics_sampling_theorem">here</a>.

## Unit step
A unit step function is a signal which is $0$ until a certain moment in time and from then on equals $1$.
The unit step function is denoted by $u[n]$ and is defined as

$$u[n] = \begin{cases} 1, &\text{for } n\geq 0 \\\ 0. &\text{elsewhere}\end{cases}$$

Fig. 1 gives a visual representation of the signal.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/unit_step.svg"
      alt="The unit step function."
    />
    <figcaption class="numbered">
      The unit step function.
    </figcaption>
  </figure>
</div>

### Shifting a unit step
An unit step can also be delayed, which inevitably results in a time shift.
This shift can be denoted by an additional term in the definition of the unit step function.
An unit step function, that is **shifted $p$ samples to the right**, is represented as

$$u[n-p] = \begin{cases} 1, &\text{for } n\geq p \\\ 0. &\text{elsewhere}\end{cases}$$

An example of a shifted unit step function is shown in Fig. 2.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/unit_step_shifted.svg"
      alt="An unit step function shifted 2 samples to the right."
    />
    <figcaption class="numbered">
      An unit step function shifted 2 samples to the right.
    </figcaption>
  </figure>
</div>

## Delta pulse
The most basic discrete-time function is the dirac delta pulse function.
The dirac delta pulse function is denoted by $\delta[n]$ and is defined as

$$\delta[n] = \begin{cases} 1, &\text{for } n = 0 \\\ 0. &\text{elsewhere}\end{cases}$$

Fig. 3 gives a visual representation of the signal.
This signal represents the value of the sample at a certain instance in time.
_It is important to note that any discrete-time signal can be represented as a linear combination of multiple shifted delta pulses._

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/delta_pulse.svg"
      alt="The dirac delta pulse function."
    />
    <figcaption class="numbered">
      The dirac delta pulse function.
    </figcaption>
  </figure>
</div>

### Shifting a delta pulse
Just as with the unit step function, a delta pulse function can also be shifted in the time domain.
A delta pulse function, that is **shifted $p$ samples to the right**, is represented as

$$\delta[n-p] = \begin{cases} 1, &\text{for } n = p \\\ 0. &\text{elsewhere}\end{cases}$$

An example of a shifted delta pulse function is shown in Fig. 4.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/delta_pulse_shifted.svg"
      alt="A delta pulse function that is shifted 3 samples to the left."
    />
    <figcaption class="numbered">
      A delta pulse function that is shifted 3 samples to the left.
    </figcaption>
  </figure>
</div>

## Pulse train
A pulse train is a sequence of equally spaced dirac delta pulses in time and is defined as

$$\delta[n-pk] = \begin{cases} 1, &\text{for } n = pk \\\ 0, &\text{elsewhere}\end{cases}$$

where $p$ is the period of the pulse train and $k$ is an integer number ($k=\ldots, -1, 0, 1, 2, \ldots$).
Fig. 5 shows an example of a pulse train with a period of 2 samples.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/pulse_train.svg"
      alt="A pulse train with a period of 2 samples."
    />
    <figcaption class="numbered">
      A pulse train with a period of 2 samples.
    </figcaption>
  </figure>
</div>


## Block wave
A block wave is a signal which equal $1$ for a limited period of time.
A block wave starting at sample $k$ and ending at sample $p$ can be represented as

$$ x[n] = \begin{cases} 1, &\text{for } k \leq n \leq p \\\ 0, &\text{elsewhere}\end{cases}$$

Fig. 6 shows an example of a block wave.
The block wave does not have a specific signal identifier and therefore we use the identifier $x$ in this example.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/block.svg"
      alt="An example of a block wave."
    />
    <figcaption class="numbered">
      An example of a block wave.
    </figcaption>
  </figure>
</div>


### Representation of delta pulses
A block wave can also be represented differently, namely as the sum of shifted delta pulses.
The left half of Fig. 7 shows a block wave decomposed in multiple delta pulses.
The example in question can therefore be written as
$ x[n] = \delta[n-1] + \delta[n-2] + \delta[n-3].$

<div style="max-width: 1000px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/basics/block_decomposed.svg"
      alt="An example of a block wave with its decomposition in terms of delta pulses and unit step functions."
    />
    <figcaption class="numbered">
      An example of a block wave with its decomposition in terms of delta pulses and unit step functions.
    </figcaption>
  </figure>
</div>

In general it holds that any arbitrary block wave with unity amplitude starting at sample $k$ and ending at sample $p$ can be represented as
$$ x[n] = \delta[n-k] + \delta[n-k-1] + \ldots + \delta[n-p + 1]+ \delta[n-p] =\sum_{m=k}^{p} \delta[n-m].$$


### Representation of unit step functions
Similarly the block wave can also be represented as the sum of two unit step functions as shown in Fig. 7.
The key trick here is to make sure that the second unit step functions cancels out the first unit step function.
In the example in question, the block wave can be written as $x[n] = u[n-1]-u[n-4]$.

In general it holds that any arbitrary block wave with unity amplitude starting at sample $k$ and ending at sample $p$ can be represented as
$$ x[n] = u[n-k] - u[n-p-1].$$
