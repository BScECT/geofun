# Hypothesis testing

## What is hypothesis testing?

The [very first section of this book](1:data_to_insight:statistics) mentions that statistics is often divided into two main branches: *descriptive* and *inferential* statistics. [In part A](1:descriptive_statistics), you saw that descriptive statistics aim at analyzing and summarizing the data while losing as little information as possible. Its goal is to better understand the observations and their variability, and to highlight any pattern in the data that might be of interest.

But data are just a sample from a [larger population](1:clt:population) and, in most cases, we are actually interested in the characteristics of that population. Take for instance a potential geothermal reservoir (the population): to know whether this reservoir is actually suitable, we need to know its properties (e.g., porosity, permeability, heat conductivity); extracting cores from boreholes (the sample) is the most direct and thorough way to get insights about those, but this operation is so expensive and difficult that drilling everywhere is impossible. So how can we be sure that the summary statistics computed from a limited number of cores give us any insight about the corresponding values for the whole population? This is where inferential statistics comes into play. Inferential statistics aims at generalizing beyond the data themselves to draw conclusions about the population.

Hypothesis testing is a set of methods for statistical inference to evaluate a hypothesis about the population based on a sample. All those methods start with us making an assumption about the population (i.e., a hypothesis), then checking whether our data would be likely if that assumption were true (this is where probability theory comes into play), and from that we decide whether we should reject our assumption or not.

```{admonition} Tip: Statistic vs. parameter
:class: tip

In inferential statistics, a statistic is a measure used to describe a sample, while a parameter is a measure used to describe a population. So when we compute the empirical mean on a sample, we compute a statistic; given enough samples, we can assume that it is an accurate estimate of the mean of the population, which is a parameter.
```

## How to conduct a hypothesis test?

In the end, conducting a hypothesis test is like judging a suspect in a criminal case. The suspect is presumed innocent (the null hypothesis), while the alternative hypothesis corresponds to guilt. The police collects evidence (the data), and a tribunal (the hypothesis test) decides whether there is enough evidence to declare the suspect guilty beyond a reasonable doubt.

If there is enough evidence, the suspect is declared guilty (we reject the null hypothesis). Otherwise, the tribunal does not declare the suspect innocent, but simply concludes that there is not enough evidence to prove guilt (we fail to reject the null hypothesis).

### Formulating a hypothesis

Hypothesis testing evaluates whether a value of a population parameter is consistent with the data, often by comparing it to another value:
  * $\theta$, which is a parameter of a population (a mean, a standard deviation, a correlation coefficient, or any other measure).
  * $\theta'$, which is either the value of the same parameter in another population or a reference value.

We have then two hypotheses:
  * The null hypothesis $H_0$ is the hypothesis that we test against the data. In many cases, it assumes the absence of an effect (e.g., no difference, no change, no relationship) in the population. So it assumes the *status quo*:

  $$
    H_0: \theta = \theta'
  $$

  * The alternative hypothesis $H_A$ (also denoted by $H_1$) represents the presence of an effect (e.g., a difference, change, or relationship) in the population. It can take three forms:
    * A two-sided test:

      $$
        H_A: \theta \neq \theta'
      $$

    * A left-tailed test:

      $$
        H_A: \theta < \theta'
      $$

    * A right-tailed test:

      $$
        H_A: \theta > \theta'
      $$

Hypothesis tests are set up so that we end up deciding whether we can reject (or not) the null hypothesis.

### Selecting a significance level

As mentioned above, hypothesis testing factors in uncertainty: we do not know the true population parameter(s), so there is always a risk that we reject the null hypothesis when it is true, or not reject it when it is false:

|                         | $H_0$ is true    | $H_0$ is false   |
| :---------------------: | :--------------: | :--------------: |
| **Do not reject $H_0$** | Correct decision | Type II error    |
| **Reject $H_0$**        | Type I error     | Correct decision |

So we are left with two potential errors:
  * The type I error, also called a false positive, which occurs with a probability $\alpha$. This error occurs when the test detects a difference that actually does not exist in the population (e.g., convicting an innocent).
  * The type II error, also called a false negative, which occurs with a probability $\beta$. This error occurs when the test fails to detect a difference that actually exists in the population (e.g., acquitting a criminal).

Before conducting the test itself, we must choose the probability of a type I error (so the probability of rejecting the null hypothesis when it is true) that we are willing to tolerate, which is called the significance level $\alpha$. This choice is case dependent, and there is often no "best" significance level. In general, three values tend to be used:
  * $\alpha = 0.05$: the universal default, which originally comes from [Ronald Fisher's work](https://doi.org/10.1007/978-1-4612-4380-9_6):
    <blockquote>The value for which P=0.05, or 1 in 20, is 1.96 or nearly 2; it is convenient to take this point as a limit in judging whether a deviation ought to be considered significant or not. Deviations exceeding twice the standard deviation are thus formally regarded as significant. Using this criterion we should be led to follow up a false indication only once in 22 trials, even if the statistics were the only guide available. Small effects will still escape notice if the data are insufficiently numerous to bring them out, but no lowering of the standard of significance would meet this difficulty.</blockquote>
    In the end, it is a bit of an arbitrary choice, and depending on the objective it is worth adjusting this value.
  * $\alpha = 0.01$: a lower tolerance for false positives is often valuable in high-stake studies, e.g., to avoid a dangerous or ineffective treatment when testing a new drug in medicine.
  * $\alpha = 0.1$: a higher tolerance for false positives is often valuable in exploratory studies, because that usually leads to less false negatives, e.g., to avoid missing a potential breakthrough whose return on investment would be worth the risk.

<!-- The probability of correctly rejecting a false null hypothesis is called the power of the test and equals $1 - \beta$. -->

### Selecting a test statistic

Hypothesis tests rely on a test statistic $t$ linked to a specific distribution model. We have then two options to conduct the test:
  * Compute one or more critical values corresponding to the chosen significance level $\alpha$ from the distribution model. We can then compare the critical value to test statistic observed from the data $t_\text{obs}$ to conclude the test.
  * Compute a $p$-value from the test statistic observed from the data $t_\text{obs}$ and the distribution model. The $p$-value is the probability of having a test statistic at least as extreme as the one we got if the null hypothesis is true. We can then compare the significance level to the $p$-value to conclude the test.

Originally, hypothesis tests were conducted based on critical values, because they were easier to obtain using [statistical tables](2:statistical_tables). But the development of computers made computing $p$-values more accessible, and since they are easier to interpret and compare, they have become the standard output in statistical software. 

### Making a decision

The outcome of a hypothesis test is a decision: either reject the null hypothesis or do not reject it. Not rejecting the null hypothesis does not mean that it is true, it only means that there is not enough evidence against it. With a critical value, this process depends on the type of test we are conducting:
  * In a two-sided test, we reject the null hypothesis when the test statistic is lower than the lower critical value (corresponding to $\frac{\alpha}{2}$) or greater than the upper critical value (corresponding to $1 - \frac{\alpha}{2}$).
  * In a left-tailed test, we reject the null hypothesis when the test statistic is lower than the critical value corresponding to $\alpha$.
  * In a right-tailed test, we reject the null hypothesis when the test statistic is greater than the critical value corresponding to $\alpha$.

With a $p$-value, we reject the null hypothesis when the $p$-value is lower than $\alpha$. This decision rule is the same for all tests, only the way the $p$-value is computed depends on the type of test:
  * In a two-sided test, we need to compute $P_{H_0}(T < -|t_\text{obs}|) + P_{H_0}(T > |t_\text{obs}|)$.
  * In a left-tailed test, we need to compute $P_{H_0}(T < t_\text{obs})$.
  * In a right-tailed test, we need to compute $P_{H_0}(T > t_\text{obs})$.

Rejecting the null hypothesis implies that the data provide sufficient evidence to support the alternative hypothesis, but this result is only statistically significant at the $\alpha$ level, and it does not prove that the alternative hypothesis is true: it only means that the data would be unlikely if the null hypothesis were correct.

## What kinds of test exist?

For this subsection, let's assume that we have a sample of $n$ observed values $\{x_1, x_2, ..., x_n\}$ of a variable $X$.

### Tests of central tendency

#### $Z$-test

In a $Z$-test, we want to assess whether the population mean $\mu_X$ is different, lower, or higher than a reference value $\mu_0$. This test is seldom used in practice because it assumes that the population variance $\sigma_X$ is known, which is rarely the case.

**Null and alternative hypotheses**

$H_0: \mu_X = \mu_0$

$H_A: \mu_X \neq \mu_0$ or $\mu_X < \mu_0$ or $\mu_X > \mu_0$

**Test statistic**

$$z = \frac{\overline{x} - \mu_0}{\frac{\sigma_X}{\sqrt{n}}}$$

Where $\overline{x}$ is the sample mean.

The test statistic follows a [normal distribution](https://distribution-explorer.github.io/continuous/normal.html) under the null hypothesis ({numref}`figure {number} <hypothesis_testing>`).

**Assumptions**

  * The population is normally distributed or the sample size is large enough for the central limit theorem to apply (then the sample mean $\overline{X}$ follows a normal distribution with mean $\mu_0$ and variance $\frac{\sigma_X^2}{n}$).
  * The population variance $\sigma_X^2$ is known.
  * The observations are independent and the sample is representative of the population.

````{iframe-figure} ../../_static/part-b_hypothesis-testing.html
---
name: hypothesis_testing
width: 825px
height: 415px
align: center
---
Change the distribution to switch between $Z$- and $t$-test, and the test and significance level to see how the rejection region(s) change(s).
````

#### $t$-test

In a $t$-test, we also want to assess whether the population mean $\mu_X$ is different, lower, or higher than a reference value $\mu_0$, but this time with an unknown population variance.

**Null and alternative hypotheses**

$H_0: \mu_X = \mu_0$

$H_A: \mu_X \neq \mu_0$ or $\mu_X < \mu_0$ or $\mu_X > \mu_0$

**Test statistic**

$$t = \frac{\overline{x} - \mu_0}{\frac{s_X}{\sqrt{n}}}$$

Where $\overline{x}$ is the sample mean and $s_X$ is the sample standard deviation:

$$s_X = \sqrt{\frac{1}{n - 1}\sum_{i=1}^n (x_i - \overline{x})^2}$$

The test statistic follows a [Student's t-distribution](https://distribution-explorer.github.io/continuous/student_t.html) under the null hypothesis ({numref}`figure {number} <hypothesis_testing>`). Compared to the normal distribution, Student's t-distribution has an extra parameter, the degrees of freedom $\nu$. The degrees of freedom reflect how many independent values are used to estimate variability, so it depends on the number of data:

$\nu = n - 1$

A low number of data means a low degrees of freedom and heavier tails than the normal distribution. This increases the probability of extreme values, making it harder to reject the null hypothesis with small samples.

**Assumptions**

  * The population is normally distributed or the sample size is large enough for the central limit theorem to apply (then the sample mean $\overline{X}$ follows a normal distribution with mean $\mu_0$ and variance $\frac{\sigma_X^2}{n}$).
  * The observations are independent and the sample is representative of the population.

#### Two-sample $t$-test

In a two-sample $t$-test, we want to assess whether the population means $\mu_{X_1}$ and $\mu_{X_2}$ are different based on two independent samples of equal variance.

**Null and alternative hypotheses**

$H_0: \mu_{X_1} = \mu_{X_2}$

$H_A: \mu_{X_1} \neq \mu_{X_2}$ or $\mu_{X_1} < \mu_{X_2}$ or $\mu_{X_1} > \mu_{X_2}$

**Test statistic**

$$t = \frac{\overline{x_1} - \overline{x_2}}{s_p{\sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}}$$

Where $n_1$ and $n_2$ are the number of data in the two samples, $\overline{x_1}$ and $\overline{x_2}$ their means, and $s_{X_1}$ and $s_{X_2}$ their standard deviations so that the pooled variance $s_p^2$ is:

$$s_p^2 = \frac{(n_1 - 1)s_{X_1}^2 + (n_2 - 1)s_{X_2}^2}{n_1 + n_2 - 2}$$

The test statistic follows a [Student's t-distribution](https://distribution-explorer.github.io/continuous/student_t.html) under the null hypothesis with a degrees of freedom $\nu$:

$\nu = n_1 + n_2 - 2$

**Assumptions**

  * The two populations are normally distributed or their sample sizes are large enough for the central limit theorem to apply.
  * The two samples are independent and the observations within each sample are independent.
  * The two populations have equal variances.
  * The samples are representative of their respective populations.

#### Welch's $t$-test

In Welch's $t$-test, we also want to assess whether the population means $\mu_{X_1}$ and $\mu_{X_2}$ are different based on two independent samples. In practice, it is often preferred over the two-sample $t$-test because it does not require equal variances.

**Null and alternative hypotheses**

$H_0: \mu_{X_1} = \mu_{X_2}$

$H_A: \mu_{X_1} \neq \mu_{X_2}$ or $\mu_{X_1} < \mu_{X_2}$ or $\mu_{X_1} > \mu_{X_2}$

**Test statistic**

$$t = \frac{\overline{x_1} - \overline{x_2}}{s_{\overline{\Delta}}}$$

Where $\overline{x_1}$ and $\overline{x_2}$ are the means of the two samples and $s_{X_1}$ and $s_{X_2}$ their standard deviations so that:

$$s_{\overline{\Delta}} = \sqrt{\frac{s_{X_1}^2}{n_1} + \frac{s_{X_2}^2}{n_2}}$$

The test statistic follows a [Student's t-distribution](https://distribution-explorer.github.io/continuous/student_t.html) under the null hypothesis with a degrees of freedom $\nu$:

$$\nu \approx \frac{\left(\frac{s_{X_1}^2}{n_1} + \frac{s_{X_2}^2}{n_2}\right)^2}{\frac{\left(\frac{s_{X_1}^2}{n_1}\right)^2}{n_1 - 1} + \frac{\left(\frac{s_{X_2}^2}{n_2}\right)^2}{n_2 - 1}}$$

**Assumptions**

  * The two populations are normally distributed or their sample sizes are large enough for the central limit theorem to apply.
  * The two samples are independent and the observations within each sample are independent.
  * The samples are representative of their respective populations.

### Tests of dispersion

#### $\chi^2$-test

In a $\chi^2$-test for the variance, we also want to assess whether the population variance $\sigma_X^2$ is different, lower, or higher than a reference value $\sigma_0^2$.

**Null and alternative hypotheses**

$H_0: \sigma_X^2 = \sigma_0^2$

$H_A: \sigma_X^2 \neq \sigma_0^2$ or $\sigma_X^2 < \sigma_0^2$ or $\sigma_X^2 > \sigma_0^2$

**Test statistic**

$$\chi^2 = \frac{(n - 1)s_X^2}{\sigma_0^2}$$

Where $s_X$ is the sample standard deviation.

The test statistic follows a [chi-squared distribution](https://distribution-explorer.github.io/continuous/chi_square.html) under the null hypothesis. The chi-squared distribution has the degrees of freedom $\nu$ as parameter, which depends on the number of data:

$\nu = n - 1$

**Assumptions**

  * The population is normally distributed.
  * The observations are independent and the sample is representative of the population.

#### $F$-test

In a $F$-test for the variance, we want to assess whether the population variances $\sigma_{X_1}^2$ and $\sigma_{X_2}^2$ are different based on two independent samples.

**Null and alternative hypotheses**

$H_0: \sigma_{X_1}^2 = \sigma_{X_2}^2$

$H_A: \sigma_{X_1}^2 \neq \sigma_{X_2}^2$ or $\sigma_{X_1}^2 < \sigma_{X_2}^2$ or $\sigma_{X_1}^2 > \sigma_{X_2}^2$

**Test statistic**

$$F = \frac{s_{X_1}^2}{s_{X_2}^2}$$

Where $s_{X_1}$ and $s_{X_2}$ are the standard deviations of the two samples.

The test statistic follows a [$F$-distribution](https://en.wikipedia.org/wiki/F-distribution) under the null hypothesis. The $F$-distribution has two degrees of freedom $\nu_1$ and $\nu_2$ as parameters, which depend on the number of data in each sample $n_1$ and $n_2$:

$\nu_1 = n_1 - 1$

$\nu_2 = n_2 - 1$

**Assumptions**

  * The two populations are normally distributed.
  * The two samples are independent and observations within each sample are independent.
  * The samples are representative of their respective populations.

### Other tests

Many more hypothesis tests have been developed beside these few examples. You can test whether a distribution is more skewed than a normal distribution, whether a sample follows a normal distribution, whether a correlation is significant, etc. To have an idea of what is possible, you can take a look at SciPy documentation: SciPy has [many functions to perform all sorts of hypothesis tests](https://docs.scipy.org/doc/scipy/reference/stats.html#hypothesis-tests-and-related-functions).

## What is $p$-hacking?

$P$-hacking means tweaking the data or the analysis to get statistically significant results ({numref}`figure {number} <slope_hypothesis_testing>`). There are [many ways to do so](https://doi.org/10.1038/d41586-025-01246-1), such as:
  * Stopping collecting data when reaching a significant result.
  * Repeating an experiment until a significant result is reached.
  * Removing some data, such as outliers, to lower the $p$-value.
  * Changing the significance level after getting the $p$-value.
  * Running multiple tests, for instance on multiple variables, and only reporting the significant ones.

````{figure} https://imgs.xkcd.com/comics/slope_hypothesis_testing.png
---
name: slope_hypothesis_testing
width: 100%
align: center
---
Example of $p$-hacking (image from [xkcd](https://xkcd.com/2533/)).
````

This is why preregistration was developed, especially for clinical trials: the idea is to submit a plan for a study &ndash; including data acquisition protocol, hypotheses, and statistical methods and analyses &ndash; before starting the study, which limits the option for tweaking the results *a posteriori*.
