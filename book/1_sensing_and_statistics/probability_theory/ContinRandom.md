# Continuous random variables

Experiments often have a noncountable infinite number of outcomes. How then to describe the probability distribution?


## Learning objectives

After studying *Continuous random variables* you will be able to ...
* define continuous random variables
* evaluate probability density functions and distribution functions of continuous random variables
* define and interpret the expectation and variance of random variables

## From histogram to probability density function

An histogram with relative frequencies based on observed data can be used to show the *empirical* distribution of the random variable.

As an example, let us consider a dataset of wind speeds in Delft. The figure below shows wind speed measurements in Delft at 10m height over the past year[^ref]. To the right of the time series is a **histogram** of the wind speeds. Observe how some wind speeds are more common than others.

````{iframe-figure} ../../_static/elements/element_empirical_wind_speed.html
:name: empirical_wind_speed
:aspectratio: 2 / 1

Wind speed measurements at 10m height in Delft over the past year. Hover over the graph to highlight individual data points. This element, and all subsequent elements on this page, access the latest available wind speed data from an online resource. If you come back later, these plots may look different.
````

Histograms showing relative frequencies can be used to calculate the empirical probability that an outcome will be inside a certain interval. However, a large amount of data is needed, and a proper bin width must be chosen to get a good representation of the actual probability distribution. This is illustrated in {numref}`figure {number} <hist_rf>` below, where the number of samples as well as the bin width has been varied. 

````{figure} ../../figures/part-a_hist_rf.png
---
name: hist_rf
width: 80%
align: center
---
Histograms with relative frequencies for varying number of samples (left to right) and bin widths (top - bottom).
````

Note that by choosing a smaller bin width, the relative frequency becomes smaller as well. This can be understood by realizing that if for instance we take half of the bin width, the outcomes in a certain bin are divided over two bins. Eventually, if we would choose a very small bin width, the relative frequencies would become very small as well. 

A solution to this problem is to work with *densities* instead of relative frequencies. 

$$
f(x_i) = \frac{p(x_i)}{\Delta x}
$$

with $f(x_i)$ the density of the bin centered at $x_i$, $p(x_i)$ the corresponding relative frequency, and $\Delta x$ the bin width. Indeed you can see that the density is (almost) insensitive to the chosen bin width, since both $p(x_i)$ and $\Delta x$ will increase (or decrease), and their ratio remains approximately the same. This is shown in {numref}`figure {number} <hist_dens>`.

````{figure} ../../figures/part-a_hist_dens.png
---
name: hist_dens
width: 80%
align: center
---
Histograms with relative frequencies for varying number of samples (left to right) and bin widths (top - bottom).
````

Ultimately, if we would have infinitesimally small bin widths, the histogram with empirical densities would approach a continuous function (for which we would need a huge amount of data), see {numref}`figure {number} <hist_pdf>`. 

````{figure} ../../figures/part-a_pdf.png
---
name: hist_pdf
width: 40%
align: center
---
Probability density function with corresponding histogram in background.
````

Fortunately, for many real-world phenomena it was found that their *probability density function* (pdf) can be described by a specific function. Before we will introduce examples of such continuous distributions, we will first look at how we can calculate probabilities from a probability density function and define the corresponding distribution function, as we did for discrete random variables. Furthermore, we will introduce the expectation and variance of random variables.

## Probability density function and distribution function

Assume we are interested in the probability $\mathsf{P}(a\leq X\leq b)$. Assuming $a$ and $b$ correspond with the edges of two bins (as in {numref}`figure {number} <prob_calc>`), and denoting the relative frequency of the bin centered at $x_i$ as $p(x_i)$, then the probability would be:

$$
\mathsf{P}(a\leq X\leq b)=\underset{x_i\in [a,b]}{\sum} p(x_i)=\underset{x_i\in [a,b]}{\sum} f(x_i)\Delta x
$$

Note that for now we ignore the fact that this is in fact an estimated probability. 

It can be seen that for the continuous pdf $f_X(x)$ this becomes:

$$
\mathsf{P}(a\leq X\leq b)=\int_a^b f_X(x)dx
$$

The probability is thus the area below the pdf as shown in the right panel of {numref}`figure {number} <prob_calc>`.

````{figure} ../../figures/part-a_probcalc.png
---
name: prob_calc
width: 80%
align: center
---
Probability $\mathsf{P}(a\leq X\leq b)$ equal to sum of relative frequencies (left) or area of bars (middle) or area below probability density function (right).
````

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Continuous random variable } X:$

A continuous random variable $X$ has a probability density function $f_X(x)$ such that:

$
\mathsf{P}(a\leq X\leq b)=\int_a^b f_X(x)dx
$

with $\int_{-\infty}^{\infty} f_X(x)dx=1$ (total probability). The distribution function is continuous and given by:

$
F_X(a)= \mathsf{P}(X\leq a) = \int_{-\infty}^a f_X(x)dx
$

This implies that $\mathsf{P}(X= a) = 0$.

</div>

Below, you find an interactive element[^ref2] that illustrates the relationship between the integral of the pdf and the cdf value. The grey-shaded area in the left subplot corresponds to the integral from $-\infty$ to $x$. Move your mouse over either the subplots and try to develop an intuition for how both distributions relate to each other. When is the cdf steep, when is it flat?

````{iframe-figure} ../../_static/elements/element_pdf_and_cdf.html
:name: pdf_cdf

Interactively visualize the relationship between the pdf and the distribution function (the integral of the pdf value). The shaded region in the left subplot represents the area integrated by the cdf.
````


[^ref]: <a href="https://open-meteo.com/">Weather data by Open-Meteo.com</a>. The API data shown here are offered under Attribution 4.0 International (CC BY 4.0). If the graph only shows data from January to December 2024, the server is currently unavailable and a backup dataset has been loaded. 

This example and the interactive element was created by Max Rambgraber, and was taken from:
 Ding, J. Lanzafame, R., van der Meer, F. van Woudenberg, T., Verhagen, S. (Eds.) (n.d.), Modelling, Uncertainty and Data for Engineers (MUDE) Textbook, Delft University of Technology. <a href="https://mude.citg.tudelft.nl/book"> CC BY 4.0</a>.

 [^ref2]: The interactive figures in these pages are created by Max Ramgraber ([maxramgraber.com/interactive](https://www.maxramgraber.com/interactive)), which are published with a CC BY license and included in this book without modification.