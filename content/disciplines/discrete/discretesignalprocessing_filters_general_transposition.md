+++
title = "Transposition theorem"

# date = {{ .Date }}
lastmod = 2020-05-02

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Transposition theorem"
  weight = 3
  parent = "Filter structures II: General filter structures"
+++


In order to realize a filter it is in practice important to have as many alternative structures available as possible.
A general method of deriving from any given structure another structure from which the input- output properties remain unchanged is based on the so-called transposition theorem.
The different steps to obtain a transposed structure
are as follows:
<ol>
  <li> Reverse direction of all branches. </li>
  <li> Change branch points ($\color{blue}{\bullet}$)into summation nodes ($\color{red}{\oplus}$)and vice versa. </li>
  <li> Interchange the input ($\color{green}{x[n]}$) and output ($y[n]$). </li>
</ol>

<div class="example">
<h4> Example </h4>
<hr>
  Apply the transition theorem to the following direct form I realization of a 3-th order transversal filter:
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/filters/general/transpose0.svg"
        alt="Transpose filter structure."
      />
    </figure>
  </div>
<button class="collapsible">Show solution</button>
<div class="content">
  The first step is to reverse the direction of all branches and the second step is to interchange branch points, as denoted in blue bullets in the figure, into summation nodes, denoted in red in the figure, and the other way around. This results into a new structure, as depicted at the left hand side of the figure below.
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/filters/general/transpose.svg"
        alt="Transposed filter structure."
      />
    </figure>
  </div>
  The third step is to interchange the input $x[n]$ and output $y[n]$, as depicted at the right hand side of the figure, which is the direct form II realization of the 3-th order transversal filter.
</div>
</div>
