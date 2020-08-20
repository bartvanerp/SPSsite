+++
title = "Part 1: Random variables and random signals"

# date = {{ .Date }}
lastmod = 2020-08-20

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.5cta0]
name = "Part 1: Random variables and random signals"
weight = 100

+++

Compared to <i>deterministic</i> signals, which can be described univocally by a mathematical formula or a well-defined rule, <i>stochastic</i> signals cannot be predicted with certainty at any given time. The uncertainty may come from several different sources; it may be due to measurement noise, interference  or artefacts; or sometimes a mathematical description may exist but it is so complex that is not practically useful.  
Although the difference between deterministic and stochastic signal may be subtle at times, due to measurement or numeric noise, almost any real-world or synthetic signal can be actually considered a random signal. The question may then arise: how do we processes such signals?
This part of the course provides the basic tools necessary to answer this question.

The topics covered in this part are:
<ul>
<li><a href="../mathematicalbackground_probability_and_rv_main">Probability and random variables:</a> The term "stochastic" comes from the Greek word for chance. In order to understand stochastic signals, a review of probability theory is necessary.
<li><a href="../statisticalsignalprocessing_signals_main">Random processes and random signals:</a> When coping with uncertainty, a deterministic signal can better be treated as a random signal. Here we discuss the statistical tools to characterize random signals.
<li><a href="../statisticalsignalprocessing_rational_main">Rational signal models:</a> Can we generate signals with desired statistical properties? Rational signal models provide an efficient representation for suitable types of random signals.
