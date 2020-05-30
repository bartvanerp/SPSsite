+++
title = "Complex numbers"

# date = {{ .Date }}
lastmod = 2019-06-04
draft = false       # Is this a draft? true/false
toc = true          # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Complex numbers [⯈]"
  parent = "Complex numbers and phasors"
  weight = 13

+++

From the discussion <a href="../mathematicalbackground_complex_numbersets">here</a> it follows that in practice there is a need to extend the set of real numbers to a set of complex numbers.
In this section we will first introduce the set of complex numbers in two different ways and we will show how complex numbers can be visualized by vectors.
Then we will introduce the concept of complex conjugation, which is important to obtain the definition of the length of a complex vector.
Furthermore we will introduce calculation rules for complex numbers, which are defined in such a way that these rules are generalizations of the calculation rules for real numbers.
Finally we show how the addition of two complex numbers can be visualized, which leads to the vectorial addition rule.

<br></br>

## Polar and Cartesian representation
### Polar notation
From the solution of the <a href="../mathematicalbackground_complex_numbersets/#derivation-2">harmonic oscillator</a> we saw that the solution to the second-order differential equation was given by a linear combination of $e^{\pm j\theta}$. The complex exponential $z=r e^{j\theta}$, with both $\theta \in \mathbb{R}$ and $r \in \mathbb{R}$, is also a valid solution of the second order differential equation. This notation is one of the two notations of a complex number and is the so-called polar notation. Using this information, the set of complex numbers can be defined as

$$ {\bf \text{Polar representation:}} \qquad\bbox[5px,border:1px solid black]{\mathbb{C} = \\{ z= r e^{j{\theta}} \ | \ r \in \mathbb{R} \mbox{ and } \theta \in \mathbb{R} \\}}$$

### Cartesian notation
In the other <a href="../mathematicalbackground_complex_numbersets/#derivation-1">intuitive example</a> we saw that a complex number could also be written in the form of $z=x+j\cdot y$, which is related to the polar notation through the <a href="../mathematicalbackground_complex_euler">Euler equations</a> as

$$z=re^{j\theta} = r\cdot\cos(\theta) + j\cdot r\cdot\sin(\theta)$$

The first term is the so-called **real part**, denoted by $\Re e \\{\cdot\\}$. The second term, which is the part after the unit $j$, is the so-called **imaginary part** which is denoted by $\Im m\\{\cdot\\}$. Both the real and imaginary part are real numbers and are given by the following expressions:

$$ \Re e \\{z \\} =  r \cos(\theta) \in \mathbb{R} \qquad \text{and} \qquad \Im m \\{z \\} =  r \sin(\theta) \in \mathbb{R}$$

Using this Cartesian notation, the set of complex numbers can be defined as

$$ {\bf \text{Cartesian representation:}} \qquad\bbox[5px,border:1px solid black]{\mathbb{C} = \\{ z=x+ j\cdot y \ | \ x \in \mathbb{R} \mbox{ and } y \in \mathbb{R} \\}}$$

### Visualisation of complex numbers
From these definitions it follows that a real number can be viewed as a complex number from which the imaginary part $\Im m$ is zero.
Thus the set of complex numbers $\mathbb{C}$ is a generalization of the set of real numbers $\mathbb{R}$.
From experience we know that real number can be represented on a one dimensional line, as depicted in Fig. 1.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/real_line.svg"
      alt="The real line."
    />
    <figcaption class="numbered">
      The real line, allowing for representation of the set of real numbers $\mathbb{R}$.
    </figcaption>
  </figure>
</div>

From the Cartesian (and thus also the polar representation) of complex numbers it follows that we need two independent axes in order to represent a complex number graphically: one for the real part of the complex number and one for the imaginary part.
In contrary to the set of real numbers, which are represented on the *real line*, complex numbers are represented in the **complex plane**.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/notation.svg"
      alt="A complex number represented in the complex plane in (a) Cartesian notation and (b) polar notation."
    />
    <figcaption class="numbered">
      A complex number represented in the complex plane in (a) Cartesian notation and (b) polar notation.
    </figcaption>
  </figure>
</div>

In Fig. 2 we visualized the complex number, both in Cartesian and polar notation, as a complex **vector** $z$ in a two dimensional plane.
The horizontal axis represents the real part of the complex vector $z$ while the projection on the vertical axis represents the imaginary part.
Thus, when using the Cartesian representation $z=x + j\cdot y$, the parameter $x$ represents the real part $\Re e \\{ z \\}$ and $ y$ represents the imaginary part $\Im m \\{ z \\}$.
On the other hand, when using the polar representation $z=re{^j\theta}$, the parameter $r$ represents the length of the complex vector $z$ and $\theta$ the (counterclockwise) angle with the (positive) real axis.

### Converting between the notations

From this it follows that for the Cartesian representation the length $r$ of the complex vector $z=x + j\cdot y$ is equal to $\sqrt{x^2 + y^2}$.
The angle, in radians, is defined as the angle between the positive x-axis of the complex plane and the point given by the coordinates ($x, y$) on the complex plane.
The angle is positive for counter-clockwise angles (upper half-plane, $y > 0$), and negative for clockwise angles (lower half-plane, $y < 0$).
In other words if we need to convert from Cartesian to Polar notation we can use the following equations:
$$ \bbox[5px,border:1px solid black]{r= \sqrt{x^2 + y^2} \mbox{ and } \theta=
\begin{cases}
\arctan (\frac{y}{x}) & \mbox{for } x > 0 \newline
\arctan (\frac{y}{x}) + \pi & \mbox{for } x < 0; y \geq 0 \newline
\arctan (\frac{y}{x}) - \pi & \mbox{for } x < 0; y < 0 \newline
\frac{\pi}{2} & \mbox{for } x=0; y > 0 \newline
-\frac{\pi}{2} & \mbox{for } x=0; y < 0 \newline
 \mbox{undetermined} & \mbox{for } x=y=0
 \end{cases}}$$

The different cases for the angle $\theta$ are required because of the ambiguity introduced by the $\arctan(\cdot)$ function.
This function does not take into account in which quadrant the complex number is located and therefore it is sometimes necessary to add $\pi$ to the angle.
On the other hand from the polar representation as depicted in Fig. 2 it follows that the projection of the complex vector $z=r e^{j\theta}$ on the real axis equals $r \cos (\theta)$, while the projection on the imaginary axis is given by $r \sin (\theta)$. Thus if we need to convert from polar to Cartesian notation we can use the following equations:
$$
\bbox[5px,border:1px solid black]{x= r \cos(\theta) \mbox{ and } y = r \sin(\theta)}
$$

<div class="example">
<h4> Example </h4>
<hr>
Convert $z = 4 e^{j\frac{3 \pi}{4}}$ to Cartesian notation $z=x+ j\cdot y$.
<button class="collapsible">Show solution</button>
<div class="content">
By using the <a href="../mathematicalbackground_complex_euler">Euler equations</a> we obtain:
\begin{eqnarray*}
{4 e^{j\frac{3 \pi}{4}}} &=& 4\cos\left(\frac{-3\pi}{4}\right) + j 4\sin\left(\frac{-3\pi}{4}\right) \\
&=& 4\cdot -\frac{1}{2}\sqrt{2} + j 4\cdot -\frac{1}{2}\sqrt{2} \\
&=& {\color{blue}-2\sqrt{2}} -j 2\sqrt{2}
\end{eqnarray*}
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Convert $z=-\frac{3}{2}\sqrt{3} + j \frac{3}{2}$ to polar notation $z = r e^{j\theta}$.
<button class="collapsible">Show solution</button>
<div class="content">
First calculate the length $r$ of the complex vector $z$ as follows:
$$
r = |z|  =\sqrt{\left(-\frac{3}{2}\sqrt{3}\right)^2 + \left(\frac{3}{2}\right)^2}
= \sqrt{\frac{27}{4} + \frac{9}{4}} = 3
$$
Since the real part of the complex vector $z$ is negative the argument can be found with the following equation:
$$
\theta = \arctan\left(\frac{\frac{3}{2}}{-\frac{3}{2}\sqrt{3}}\right)+\pi
= \arctan\left(-\frac{1}{\sqrt{3}}\right)+\pi
= -\frac{\pi}{6} + \pi = \frac{5}{6}\pi
$$
Concluding we obtain:
$$
z ={-\frac{3}{2}\sqrt{3}} + j \frac{3}{2} = {3 e^{j\frac{5}{6}\pi}}
$$
</div>
</div>

<br></br>

## Mathematical operations
Similar to each extension from one set of numbers to a more general set of numbers, the calculation rules for complex numbers are defined in such a way that these rules generalize the calculation rules of real numbers.

Because of the fact that we can represent a complex number in Cartesian or in polar notation, each of the calculation rules can be performed by using both of these representations, however a general rule of thumb for the calculation rules is:

___It is easiest to use Cartesian notation when adding or subtraction complex numbers, while polar notation works easiest for multiplication and division.___

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/krp-1XQC0pQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Complex conjugation
In this subsection we will show that we can obtain the length of a complex vector by using the so called complex conjugated vector, denoted by $z^{\*}$, which is constructed by inverting the sign the imaginary part, so by changing j to -j and -j to j, thus:
$$\begin{eqnarray}
z = e^{j\theta} & \Rightarrow & \boxed{z^* = e^{-j\theta}} \newline
z=x + j\cdot y & \Rightarrow & \boxed{z^* = x - j \cdot y}
\end{eqnarray}$$

This conjugation operation is visualized in Fig. 3 and simply corresponds to the mirroring of the complex number in the real axis.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/conjugation.svg"
      alt="The complex conjugation operation."
    />
    <figcaption class="numbered">
      Visualisation of the complex conjugation operation.
    </figcaption>
  </figure>
</div>

We have seen that the length of a complex vector is either given by the parameter $r$, when using polar notation, or by $\sqrt{x^2+y^2}$, when using the Cartesian notation. Since the length of a vector is always a positive real number, we will denote it by using the absolute value sign $| \cdot |$. Now by using the definition of complex conjugation we can define the length of a complex vector $z$ as follows:
$$ \bbox[5px,border:1px solid black]{|z| = \sqrt{z \cdot z^* }} \qquad \text{real and } \geq 0 $$

This definition can be shown either by using polar or Cartesian notation as follows:
$$ \begin{eqnarray}
|z| &=& \sqrt{r e^{j\theta} \cdot r e^{-j\theta}} = \sqrt{r^2 e^{j(\theta - \theta)}} = r \newline
&=& \sqrt{(x + j\cdot y) \cdot (x - j\cdot y)} = \sqrt{x^2 - j xy + j y x - j^2 y^2}= \sqrt{x^2 + y^2}
\end{eqnarray} $$


### Addition & subtraction
When adding two complex numbers $z_1=x_1 + j y_1$ and $z_2=x_2 + j y_2$ we have to add **separately** their real parts and imaginary parts. Thus when evaluating the real and imaginary part of $z=z_1 + z_2$ we obtain:
$$ z=z_1 + z_2 = (x_1 + j y_1) + (x_2 + j y_2) = (x_1+x_2) + j (y_1 + y_2)$$
from which it follows that:
$$ \Re e\\{z\\} = x_1 + x_2 \qquad \text{and} \qquad \Im m\\{z\\} = y_1 + y_2 $$

As a result of the separate addition of the real and the imaginary parts we can visualize the addition of two complex vector by the so called vector addition rule which is depicted in Fig. 4.
Now because of the fact that we have to add the real and imaginary parts separately.
The construction of the addition of two complex vectors in a resulting complex vector $z$ is simply performed by appending the vectors behind each other.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/addition.svg"
      alt="The complex addition operation."
    />
    <figcaption class="numbered">
      Visualisation of the complex addition operation.
    </figcaption>
  </figure>
</div>

### Multiplication
The result $z=r e^{j\theta}$ of multiplying two complex vectors $z_1=r_1 e^{j\theta_1}$ and $z_2=r_2 e^{j\theta_2}$ is:
$$ z =  z_1 \cdot z_2 = r_1 e^{j\theta_1} \cdot r_2 e^{j\theta_2} = (r_1 \cdot r_2 ) e^{j(\theta_1 + \theta_2)} = r e^{j\theta} $$
with $r=r_1 \cdot r_2$ and $\theta=\theta_1 + \theta_2$.

<div class="example">
<h4> Example </h4>
<hr>
Use the Cartesian notation to find the result of the multiplication of two arbitrary complex numbers.
<button class="collapsible">Show solution</button>
<div class="content">
When using the Cartesian notation the result becomes as follows:
$$\begin{eqnarray}
z & = & z_1 \cdot z_2 = \left( x_1 + j y_1 \right) \cdot \left( x_2 + j y_2 \right) \newline
&=& x_1 x_2 + j^2 y_1 y_2 + j x_1 y_2 + j y_1 x_2 \newline
&=& (x_1 x_2 - y_1 y_2) + j \cdot( x_1 y_2 + x_2 y_1) \newline
&=& \Re e \{ z \} + j \cdot \Im m \{ z \}
\end{eqnarray}$$
</div>
</div>


### Division
The result $z=r e^{j\theta}$ of dividing two complex vectors $z_1=r_1 e^{j\theta_1}$ and $z_2=r_2 e^{j\theta_2}$ is:
$$ z =  \frac{z_1}{z_2} = \frac{r_1 e^{j\theta_1}}{r_2 e^{j\theta_2}} = \frac{r_1}{r_2} \cdot e^{j(\theta_1 - \theta_2)} = r e^{j\theta} $$
with $r=\frac{r_1}{r_2}$ and $\theta=\theta_1 - \theta_2$.

<div class="example">
<h4> Example </h4>
<hr>
Use the Cartesian notation to find the result of the division of two arbitrary complex numbers.
<button class="collapsible">Show solution</button>
<div class="content">
When using the Cartesian notations $z_1 = x_1 + j y_1$ and $z_2=x_2 + j y_2$ for dividing two complex numbers the main problem is that there is a complex number in the denominator. So we have to find a way to get rid of this complex number in the denominator. Now we have seen before that when multiplying a complex number by its complex conjugate the result is real. We can use this fact to rewrite the original fraction of two complex numbers as a fraction of a complex number divided by a real number. This strategy goes as follows:
$$
z = \frac{z_1}{z_2} = \frac{z_1}{z_2} \cdot 1 = \frac{z_1}{z_2} \cdot \frac{z_2^*}{z_2^*} =
\frac{z_1 \cdot z_2^*}{|z_2|^2}
$$
Now the division works out as follows:
$$ \begin{eqnarray}
z & = & \frac{z_1}{z_2} = \frac{z_1 \cdot z_2^*}{|z_2|^2} =
\frac{x_1 x_2 - j^2 y_1 y_2 - j x_1 y_2 + j y_1 x_2}{x_2^2 + y_2^2}\newline
&=& \frac{(x_1 x_2 + y_1 y_2) + j (y_1 x_2 - x_1 y_2)}{x_2^2 + y_2^2} \newline
&=& \left ( \frac{x_1 x_2 + y_1 y_2}{x_1^2 + y_1^2} \right) + j \left (
\frac{y_1 x_2 - x_1 y_2}{x_1^2 + y_1^2} \right ) = \Re e \{ z \} + j \Im m \{ z \}
\end{eqnarray} $$
</div>
</div>
