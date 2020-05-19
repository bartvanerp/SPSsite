+++
title = "Probability and random variables"

# date = {{ .Date }}
lastmod = 2019-12-30

draft = false       # Is this a draft? true/false
toc = true         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Probability and random variables"
  weight = 50

+++

## Introduction

Most of the fundamentals tools in signal processing, e.g., the rules of convolution, the Z- and Fourier transforms, digital filter designs, are based on the framework of deterministic signal processing. However, when uncertainty is involved, deterministic approaches are not suitable.
Uncertainty is almost always present in the world around us. A very simple example where uncertainty plays an import role is the weather forecast. The weather forecast makes a prediction of the weather in the days ahead. However, this prediction does not guarantee that the predicted event actually takes place. Probability theory provides the mathematical tools to reason when uncertainty is present.

In signal processing we deal with measured signals which are often not ideal. Usually the signals are corrupted by noise and the exact values of this noise at certain moment in time cannot be determined. A common source of noise is thermal noise, originating from the electronic components in the measurement equipment. Electronic components inevitably generate noise, because of the free electrons in the materials. These electrons have a certain energy, which is related to the temperature of the material. A higher temperature means that the electrons have a higher energy content. This energy is usually in the form of kinetic energy, meaning that the free electrons have a certain velocity associated with them. Only at a temperature of 0 Kelvin the electrons do not have kinetic energy and therefore they do not move. This random electron movement occurring at non-zero temperatures leads to small local voltage differences, which distorts the signal that is being measured and is commonly known as thermal noise.

Probability theory provides us with the tools in order to still make sense of signals with a random component. This module will discuss the main concepts behind probability theory that we need in order to process these signals.

## Module overview
The concepts covered in this module are:

1. <a href="../mathematicalbackground_probability_definitions">Definitions of probability</a> - In order to describe how uncertainty affects experiments some general definitions are clarified. Furthermore the basic theory of probability theory is explained.
2. <a href="../mathematicalbackground_probability_variables">Random variables</a> - Calculations with uncertainty involve so-called random variables. These random variables have specific characteristics and allow us to solve problems involving uncertainty.
3. <a href="../mathematicalbackground_probability_functions">Functions and pairs of random variables</a> - Random variables are often not present in their simplest form. Problems usually involve functions of random variables and/or multiple random variables.
4. <a href="../mathematicalbackground_probability_families">Families of random variables</a> - Some processes can be described by random variables following very specific and well-known functions. These common functions and their characteristics are called the families of random variables.
5. <a href="../mathematicalbackground_probability_vectors">Random vectors</a> - Usually a random process involves multiple parameters. Multiple random variables can be concatenated into a single random vector, which greatly simplifies the notation and allows for more exotic operations.
