# Law of large numbers and central limit theorem


(1:clt:population)=
## Random sample and population

In statistics, the *population* refers to the complete set of all objects / people of interest, e.g.,

* all wind turbines in wind farms at the North Sea
* all glaciers in the Alps
* all geothermal wells in The Netherlands
* all EC&T students of cohort 2025-2026

In practice, we won't be able to get data about the full population, so best we can do is to make inferences about the properties of the population based on a *random sample*, which is a subset from the population. Thereby it is important to use a representative and large enough sample to avoid sampling biases. In the following we will look more closely at the effect of the sample size.

## Independent identically distributed (i.i.d.) random variables

Random variable $𝑋_1$ and $X_2$ are independent if $\mathsf{P}\left(X_1\in S,X_2\in T\right)= \mathsf{P}\left(X_1\in S)\mathsf{P}(X_2\in T\right)$ (in line with $\mathsf{P}(A\cap B)= \mathsf{P}(A)\mathsf{P}(B)$). In words: the outcome of one does not affect the other.

For the sum of $n$ independent random variables $X_i$, $Y=\sum_{i=1}^{n}X_i$, we have:

$\mathbb{E}\left(Y\right)=\sum_{i=1}^{n}\mathbb{E}\left(X_i\right)$

$Var(Y)=\sum_{i=1}^{n}Var\left(X_i\right)$

If independent also have exactly the same probability distribution (so also with same values for the parameters of the distribution), the we will call them *independent identically distributed* (i.i.d.).


## Law of large numbers

Recall that one cause of epistemic uncertainty are random measurement errors. Taking the average of repeated measurements helps to reduce this uncertainty... This is an example of the *law of large numbers*.

More generally, the law of large numbers states that if the size of our random sample increases, its mean will approximate the average of the whole population better.

For the law of large numbers to hold we need that:

* the subsequent experiments are performed under identical conditions, i.e., the outcome of each experiment is identically distributed,
* and do not influence each other, i.e., outcomes are independent.

A sequence of experiments will then result in of $X_i$ which are i.i.d. If the $X_i$ have expectation $\mu$ and variance $\sigma^2$, what will then be the mean and variance of ${\overline{X}}_n=\frac{1}{n}\sum_{i=1}^{n}X_i$? Try to show yourself that:

$\mathbb{E}\left({\overline{X}}_n\right)=\mu$

$Var({\overline{X}}_n)=\frac{\sigma^2}{n}$

This shows that the *sample mean* is equal to the expectation of the individual $X_i$, and that the variance of the sample mean decreases with $n$. So indeed, the uncertainty (variance) is reduced if we take the mean of many outcomes!

A smaller variance means smaller spread in outcomes, hence it is expected that an outcome will be closer to the mean. This implies that the probability that $|{\overline{X}}_n-\mu|$ will be larger than a certain value will become smaller as well.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Law of large numbers:}$

Let $X_1,X_2,\ldots,X_n$ be i.i.d. with expectation $\mu$ and variance $\sigma^2$ (both finite).

For the sample mean $\overline{X}_n=\frac{1}{n}\sum_{i=1}^n X_i$ we have that for any $\epsilon>0$:

$\underset{n\rightarrow\infty}{\lim}{P(|{\overline{X}}_n-\mu|>\epsilon)\mathrm{=0} }$

</div>


## Central limit theorem

The Central Limit Theorem (CLT) states that the distribution of the sample mean approaches a normal distribution with increasing sample size, even if underlying distribution of the individual $X_i$ is non-normal. This allows to make inferences about statistical properties by using the normal distribution to approximate probabilities of events.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Central limit theorem (sum):}$

Let $X_1,X_2,\ldots,X_n$ be i.i.d. with expectation $\mu$ and variance $\sigma^2$ (both finite).

For large $n$ the sum $Y=\sum_{i=1}^n X_i$ approximately has a normal distribution:

$Y\overset{d}{\sim}N(n\mu,n\sigma^2)$

</div>

If the $X_i$ are normally distributed, the result is exact, otherwise it is an approximation, indicated by the $\overset{d}{\sim}$.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Central limit theorem (mean):}$

Let $X_1,X_2,\ldots,X_n$ be i.i.d. with expectation $\mu$ and variance $\sigma^2$ (both finite).

For large $n$ the sample mean $\bar{X}_n=\frac{1}{n}\sum_{i=1}^n X_i$ approximately has a normal distribution:

$\bar{X}_n\overset{d}{\sim}N(\mu,\frac{\sigma^2}{n})$

</div>

:::{card} Exercise

<iframe src="https://tudelft.h5p.com/content/1292834068460666597/embed" aria-label="LLN" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292834097371062027/embed" aria-label="clt2" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292834049417637987/embed" aria-label="CLT" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::