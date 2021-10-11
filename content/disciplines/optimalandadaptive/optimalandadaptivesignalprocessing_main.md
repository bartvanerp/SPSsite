+++
title = "Optimal and adaptive signal processing"         # name of webpage

# date = {{ .Date }}
lastmod = 2019-05-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.optimalandadaptive]                       # name of menu section (main module)
  name = "Optimal and adaptive signal processing: overview"        # name of this item in that menu
  weight = 10                           # location in that menu

+++


The concepts covered in this discipline are:

1. <a href="../optimalandadaptivesignalprocessing_wiener_main">Optimal Wiener filters</a> - One of the questions that might come up when designing a filter is: what is the ideal filter? Under some assumptions, the answer to this question is given by the Wiener filter.

2. <a href="../optimalandadaptivesignalprocessing_adaptive_main">Adaptive filters</a> - When processing and analyzing signals, it is possible that the parameters of the signal are time-varying. Because of this reason, it is not possible to determine a perfect algorithm beforehand, but instead it is important to create an algorithm which continuously updates itself.
