+++
title = "Quantization and overflow"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Quantization and overflow"
  weight = 2
  parent ="Finite word length effects"

+++


In performing computations with a fixed- or floating-point digital processor, it is necessary to quantize numbers. Furthermore we have to take care about overflow,  which is the phenomenon when the quantity $x$ has a value which is larger than the available boundaries to represent numbers.

<br></br>
## Quantization
Quantization is the process in which the number $x$ is represented by another number $\hat{x}$, which is roughly equal to the value of $x$, but $\hat{x}$ can take less different values than $x$. The difference between these two numbers is the error $e=\hat{x}-x$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/quantization.svg"
      alt="Three common quantization characteristics."
    />
    <figcaption class="numbered">
      Three common quantization characteristics.
    </figcaption>
  </figure>
</div>
With quantization step $q$ the Fig. 1 shows three common quantization characteristics: Rounding, Value truncation and  Magnitude truncation.

Furthermore it is noted that quantization is a non-linear operation since the quantized result of an addition of two numbers $x$ and $y$ is not equal to the addition of the two individual quantized results, thus
$$
\widehat{x+y} \neq \hat{x} + \hat{y}
$$

<br></br>
## Overflow
Another form of non-linearity that we can deal with is what we refer to as the concept of overflow,  which is the phenomenon when the quantity $x$ has a value which is larger than the available boundaries to represent numbers, denoted by plus or minus the value $A$. The relation between $x$ and its truncated version $\hat{x}$ is called the overflow characteristic.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/overflow.svg"
      alt="Three common overflow characteristics."
    />
    <figcaption class="numbered">
      Three common overflow characteristics.
    </figcaption>
  </figure>
</div>
Fig. 2 shows three common overflow characteristics:
Saturation,  Nulling and  Sawtooth overflow.
