+++
title = "Binary Representation of numbers"

# date = {{ .Date }}
lastmod = 2020-05-31

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Binary representation of numbers"
  weight = 1
  parent ="Finite word length effects"

+++

There are roughly two ways for representing numbers in a digital system: Fixed point and floating point.

## Fixed point representation
In the fixed point representation there are three commonly used formats: Sign magnitude, One's complement and Two's complement. In these representations, the only difference can be found in the way that negative numbers are represented.  A binary number is represented by $B$ bits, in which each of the bits $b_i$ are either 0 or 1.  Bit $b_0$ is the sign bit, with a 0 indicating a positive number and 1 a negative number. The remaining bits represent the magnitude, with bit $b_1$ the Most Significant Bit, abbreviated as MSB, and the last bit the Least Significant Bit, abbreviated as LSB.
<ul>
 <li> <i> Sign Magnitude (SM): </i> The following equation shows the general binary sign magnitude representation of a decimal number:
 $$
 \color{red}{(-1)^{b_0}} \sum_{i=1}^{B-1} b_i 2^{B-1-i}
 $$
 </li>
 <li> <i> One's complement (1C): </i> In one's complement representation, a negative number is represented by complementing, that is interchanging a $0$ by a $1$ and vice versa, all of the bits in the binary representation of a positive number. </li>
 <li> <i> Two's complement (2C): </i> In two's complement representation, negative numbers are formed by complementing the bits of the positive number and adding 1 to the Least Significant Bit. </li>
</ul>

In a similar way we can represent the decimal fraction with a number of bits in which the first bit after the decimal point represents the number $2^{-1}$.



<div class="example">
<h4> Example </h4>
<hr>
Give for all three binary representations SM, 1C and 2C, the 5 bits binary representation of the positive and negative number 11. Give also the 8 bits binary representation of the positive and negative number $3.625$, in which the last 3 bits are used to represent the decimal fraction.
<button class="collapsible">Show solution</button>
<div class="content">
The table shows in columns 2 and 3 the $B=5$ bit representation of the positive and negative number $11$. Columns 4 and 5 show the 8 bit representation of the positive and negative number $3.625$, in which the last 3 bits are used to represent the decimal fraction.
<table style="width:100%">
  <tr>
    <th></th>
    <th>11</th>
    <th>-11</th>
    <th>3.625</th>
    <th>-3.625</th>
  </tr>
  <tr>
    <td>SM</td>
    <td>$\color{red}{0}1011$</td>
    <td>$\color{red}{1}1011$</td>
    <td>$\color{red}{0}0011.101$</td>
    <td>$\color{red}{1}0011.101$</td>
  </tr>
  <tr>
    <td>1C</td>
    <td>$\color{red}{0}1011$</td>
    <td>$\color{red}{1}0100$</td>
    <td>$\color{red}{0}0011.101$</td>
    <td>$\color{red}{1}1100.010$</td>
  </tr>
  <tr>
    <td>2C</td>
    <td>$\color{red}{0}1011$</td>
    <td>$\color{red}{1}0101$</td>
    <td>$\color{red}{0}0011.101$</td>
    <td>$\color{red}{1}1100.011$</td>
  </tr>
</table>
</div>
</div>





<br></br>
## Floating point representation
The following equation shows a typical floating point representation:
\begin{equation}\label{Eq:FloatingPoint}
x=M \cdot 2^{E} \hspace{5mm} \mbox{ with } \frac{1}{2} \leq |M| < 1
\end{equation}
The exponent $E$ is a positive or negative integer number. Both the mantissa $M$ and the exponent $E$ are represented as a binary word in one of the previous discussed fixed point representations in which the mantissa $M$ has only one bit (the sign bit) before the decimal point. Both words $M$ and $E$ together represent the decimal number.

<div class="example">
<h4> Example </h4>
<hr>
Give the floating point representation of the number $+3.5$ with  a 4 bit Mantissa and a 3 bit Exponent
<button class="collapsible">Show solution</button>
<div class="content">
The number 3.5 is first written as (+0.875) times $2^2$, which results with a 4 bit Mantissa and a 3 bit Exponent in the given binary representation of 0.111 010
</div>
</div>

<br></br>
## Comparison fixed and floating point representation
<ul>
  <li> <i> Dynamic range: </i> The main advantage of Floating point representation is that the range over which we can represent numbers is much larger than with fixed point numbers. </li>
  <li> <i> Resolution: </i> The resolution for a fixed point representation is constant over the whole range of numbers. The resolution of floating point number representation varies over the entire range of numbers. </li>
  <li> <i> Processors: </i> Manipulations with floating point numbers are more complicated compared to fixed point manipulations. For example when multiplying two floating point numbers we must multiply both mantissa's and add the exponents. Then we have to fit the result into the general floating point expression (\ref{Eq:FloatingPoint}). Furthermore, when adding two floating point numbers we first have to make the exponents of both numbers the same. Then we can add the mantissa's and finally we have to fit the result into the general floating point expression (\ref{Eq:FloatingPoint}). As a result Fixed point processors are typically faster and less expensive compared to floating point processors. </li>
</ul>
