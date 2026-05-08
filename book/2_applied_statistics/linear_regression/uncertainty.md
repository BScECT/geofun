(uncertaintyreg)=
# Uncertainty in regression

## What are confidence intervals?

When we estimate a parameter, we often get a single, most-likely value. But since we work from samples with a limited number of observations, there is uncertainty around that estimate. And we can also quantify that uncertainty. This is often done through confidence intervals. A confidence interval is a range of values likely to contain the true value of the parameter. More specifically, the 100$\gamma$% confidence interval for the parameter $\theta$ related to a variable $X$ is the interval $\left[\theta_l\left(X\right),\theta_u\left(X\right)\right]$ such that:

$$
    P_\theta\left(\theta_l\left(X\right)\leq\theta\leq\theta_u\left(X\right)\right) = \gamma = 1 - \alpha
$$

Most of the time, we compute the 95% confidence interval, where $\gamma = 0.95$. Note that, here, $\theta$ represents the true value of the parameter, so it is fixed, and $\theta_l\left(X\right)$ and $\theta_u\left(X\right)$ are random variables that need to be estimated from the data. So, after estimation, we get $\left[\hat{\theta}_l,\hat{\theta}_u\right]$ and, since $\theta$, $\hat{\theta}_l$, and $\hat{\theta}_u$ are all values, either $\theta$ lies between $\hat{\theta}_l$ and $\hat{\theta}_u$ or it does not, i.e.:

$$
    P_\theta\left(\hat{\theta}_l\leq\theta\leq\hat{\theta}_u\right) = 0 \text{ or } 1
$$

While a common interpretation is that the true parameter value lies within the interval with a probability of $\gamma$, the probability above shows that this is strictly speaking not true. A more accurate interpretation is that, over repeated sampling, 100$\gamma$% of the estimated confidence intervals will contain the true value. That idea of repeated sampling is key in estimating confidence intervals.

### Confidence interval for the mean with a known variance

To get an idea of how to estimate confidence intervals, let's take a look at the mean $\mu$. If we have $n$ samples represented by a set of random variables $X_1, \ldots , X_n$, each with a mean of $\mu$ and a variance of $\sigma^2$, then the sample mean is:

$$
    \overline{X} = \frac{1}{n}\sum_{i=1}^n X_i
$$

And has a mean of $\mu$ and a variance of $\frac{\sigma^2}{n}$.

:::{card} Definition

While the standard deviation $s_X$ estimates the amount of variation around the mean of a variable $X$, the standard error estimates the amount of variation around the estimate of a parameter. When that parameter is the mean itself, we have:

$$
    s_\overline{X} = \frac{s_X}{\sqrt{n}}
$$
:::

Now, let's assume that $\overline{X}$ is normally distributed and that $\sigma$ is known, and standardize $\overline{X}$:

$$
    Z = \frac{\overline{X} - \mu}{\frac{\sigma}{\sqrt{n}}}
$$

Then we have for $Z$:

$$
    P\left(-z_{\alpha/2}\leq Z \leq z_{\alpha/2}\right) = \gamma = 1 - \alpha
$$

Substituting with the definition of $Z$ leads to:

$$
    P\left(\overline{X} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}} \leq \mu \leq \overline{X} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right) = \gamma
$$

So the estimate of the 100$\gamma$% confidence interval for the mean is:

$$
    \left[\overline{x} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}}, \overline{x} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right]
$$

Which can also be written as:

$$
    \overline{x} \pm z_{\alpha/2}\frac{\sigma}{\sqrt{n}}
$$

Where $z_{\alpha/2}$ can be determined from the [table of critical values for the standard normal distribution](2:statistical_tables:normal).

In practice, this estimator holds if:
  * The population is normally distributed or the sample size is large enough for the [central limit theorem](1:clt:clt) to apply. In this later case, we get an approximate confidence interval.
  * The variance of the population is known.

### Confidence interval for the mean with an unknown variance

When the population variance $\sigma^2$ is unknown (and in most cases it is), the procedure remains the same, we just use the sample variance $s_X^2$ with Student's $t$-distribution (instead of the normal distribution). So we start by "studentizing" $\overline{X}$:

$$
    T = \frac{\overline{X} - \mu}{\frac{s_X}{\sqrt{n}}}
$$

Then we have for $T$:

$$
    P\left(-t_{n-1,\alpha/2}\leq T \leq t_{n-1,\alpha/2}\right) = \gamma = 1 - \alpha
$$

Where $n-1$ corresponds to the degrees of freedom. Substituting with the definition of $T$ leads to:

$$
    P\left(\overline{X} - t_{n-1,\alpha/2}\frac{s_X}{\sqrt{n}} \leq \mu \leq \overline{X} + t_{n-1,\alpha/2}\frac{s_X}{\sqrt{n}}\right) = \gamma
$$

So the estimate of the 100$\gamma$% confidence interval for the mean is:

$$
    \left[\overline{x} - t_{n-1,\alpha/2}\frac{s_X}{\sqrt{n}}, \overline{x} + t_{n-1,\alpha/2}\frac{s_X}{\sqrt{n}}\right]
$$

Which can also be written as:

$$
    \overline{x} \pm t_{n-1,\alpha/2}\frac{s_X}{\sqrt{n}}
$$

Where $t_{n-1,\alpha/2}$ can be determined from the [table of critical values for Student's $t$-distribution](2:statistical_tables:student).

In practice, this estimator holds if the population is normally distributed or the sample size is large enough for the [central limit theorem](1:clt:clt) to apply. In this later case, we get an approximate confidence interval again. This is all very similar to hypothesis testing, except that the output is slightly different.

## How to determine confidence intervals in linear regression?

For this subsection, we will focus on a simple linear model:

$$y = \beta_0 + \beta_1 x + \epsilon$$

Where:
  * $y$ is the outcome.
  * $x$ is the predictor.
  * $\beta_0$ and $\beta_1$ are the parameters, respectively the intercept and the slope.
  * $\epsilon$ is the error.

(2:uncertainty:parameters)=
### For the parameters

Getting confidence intervals for the slope and intercept is very similar to getting confidence intervals for a mean: the only difference is how we compute the standard error. For that, we first need to define the estimate for the variance of the error:

$$
    \hat{\sigma}_\epsilon^2 = s_\epsilon^2 = \frac{\sum_{i=1}^n (y_i - \hat{y}_i)^2}{n-2} = \frac{S_{\text{res}}}{n-2}
$$

The $n-2$ comes from loosing two degrees of freedom from having to estimate two parameters (the intercept and the slope) to get $\hat{y}_i$ (the general formula is $n - m - 1$, where $m$ is the number of predictors). This estimate is only valid if the error is normally distributed.

Then the standard error for the slope is:

$$
    s_{\hat{\beta}_1} = \frac{s_\epsilon}{\sqrt{\sum_{i=1}^n (x_i - \overline{x})^2}}
$$

And the standard error for the intercept is:

$$
    s_{\hat{\beta}_0} = s_{\hat{\beta}_1}\sqrt{\frac{1}{n}\sum_{i=1}^n x_i^2}
$$

Finally, using Student's $t$-distribution again, we get the following estimates for the 100$\gamma$% confidence intervals of the slope and the intercept:

$$
    \begin{align}
        \hat{\beta}_1 &\pm t_{n-2,\alpha/2} \times s_{\hat{\beta}_1} \\
        \hat{\beta}_0 &\pm t_{n-2,\alpha/2} \times s_{\hat{\beta}_0} \\
    \end{align}
$$

Where $\gamma = 1 - \alpha$.


```{admonition} Link to linear algebra
:class: tip

Now let's switch to a multiple linear model with $m$ predictors, here in matrix form:

$$\boldsymbol{y} = \boldsymbol{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

Where:
  * $\boldsymbol{y}$ is the observation vector and includes the outcome.
  * $\boldsymbol{X}$ is the design matrix and includes the predictors with a column of 1 for the intercept.
  * $\boldsymbol{\beta}$ is the parameter vector.
  * $\boldsymbol{\epsilon}$ is the error vector.

The estimate of the error variance becomes:

$$
    \hat{\sigma}_\epsilon^2 = s_\epsilon^2 = \frac{\sum_{i=1}^n (y_i - \hat{y}_i)^2}{n-m-1} = \frac{S_{\text{res}}}{n-m-1}
$$

Rather than the standard error, let's define $c_{jj}$, the j$^\text{th}$ element of the matrix $\left(\boldsymbol{X}^T\boldsymbol{X}\right)^{-1}$:

$$
    c_{jj} = \left(\boldsymbol{X}^T\boldsymbol{X}\right)^{-1}_{jj}
$$

Then the confidence interval for the j$^\text{th}$ parameter in $\boldsymbol{\beta}$ is:

$$
    \hat{\beta}_j \pm t_{n-m-1,\alpha/2} \times s_\epsilon \sqrt{c_{jj}}
$$
```

### For the outcome

The same procedure applies to the outcome, for which we can get two types of intervals:
  * Confidence intervals reflect the uncertainty around the mean response.
  * Prediction intervals reflect the uncertainty around the predictions, so they include mean response and error.

This implies that confidence intervals for $\hat{y}$ are narrower than prediction intervals.

The standard error for the confidence interval at a given predictor value $x$ is:

$$
    s_{\hat{y}}(x) = s_\epsilon\sqrt{\frac{1}{n} + \frac{(x - \overline{x})^2}{\sum_{i=1}^n (x_i - \overline{x})^2}}
$$

And the standard error for the prediction interval at a given predictor value $x$ is:

$$
    s_{\hat{y}}(x) = s_\epsilon\sqrt{1 + \frac{1}{n} + \frac{(x - \overline{x})^2}{\sum_{i=1}^n (x_i - \overline{x})^2}}
$$

In both cases, the interval itself is estimated with:

$$
    \hat{y} \pm t_{n-2,\alpha/2} \times s_{\hat{y}}(x)
$$

```{admonition} Link to linear algebra
:class: tip

With a multiple linear regression and $m$ predictors, the confidence interval becomes:

$$
    \hat{y} \pm t_{n-m-1,\alpha/2} \times s_\epsilon \sqrt{\boldsymbol{X}_0^T\left(\boldsymbol{X}^T\boldsymbol{X}\right)^{-1}\boldsymbol{X}_0}
$$

Where $\boldsymbol{X}_0$ is a vector of predictor values:

$$
    \boldsymbol{X}_0 =
    \begin{bmatrix}
        1 & x_{1,1} & \cdots & x_{m,1} \\
    \end{bmatrix}
$$

Similarly, the prediction interval becomes:

$$
    \hat{y} \pm t_{n-m-1,\alpha/2} \times s_\epsilon \sqrt{1 + \boldsymbol{X}_0^T\left(\boldsymbol{X}^T\boldsymbol{X}\right)^{-1}\boldsymbol{X}_0}
$$
```

### Resampling and the bootstrap

One of the assumptions of linear regression is that the mean of the error $\epsilon$ is 0 (this is necessary to get unbiased estimates of the parameters). To get confidence intervals, we have also assumed that the error is normally distributed. So in the end we have:

$$
    \epsilon \sim N(0, \sigma_\epsilon^2)
$$

This is called a parametric approach, because it relies on a model (here a normal distribution) with parameters (here a mean and a variance). Parametric approaches are efficient and precise, but only if their assumptions are met. The normality assumption is convenient because we can derive closed-form solutions for many operations, like estimating confidence intervals. But in reality we have no real reason to assume normality of the error. The central limit theorem relaxes that assumption, but what if we only have few data? What is a big enough sample anyway?

Remember that repeated sampling is at the heart of computing confidence intervals. Under the normality assumption, this was translated as treating the samples as random variables. Another approach consist in creating artificial samples from our data and estimating a parameter of interest from those. The process of extracting new samples from a dataset is called resampling, and bootstrapping or the bootstrap is a process that uses resampling to estimate a parameter.

The bootstrap is similar to the simulation procedure you have seen in part A:
  1. Extract a random sample from the data with replacement.
  1. Estimate a parameter and store its value.
  1. Repeat the operation as many times as possible.

Sampling with replacement means that the same observation can be selected multiple times (so some observations may appear multiple times in a given random sample, while others not at all). Each random sample must have the same number of observations as the original dataset. Replacement and same number of observations ensure that we mimic the process of acquiring the original dataset: we sampled from the population distribution, and a single value from that distribution can appear multiple times. Putting all the estimates from the bootstrap together, we get a sampling distribution for a parameter. We can visualize that distribution using an histogram, and compute confidence intervals using [quantiles](1:descriptive_statistics:quantiles).

The bootstrap is a non-parametric approach: it does not assume a specific model for the uncertainty around an estimate of a parameter. So it is more flexible than the normality assumption. It can also be used with any parameter or statistic: a mean, a quantile, a correlation coefficient, a slope, an intercept, even a coefficient of determination.

## How to determine the significance of a linear model?

In addition to confidence intervals, we can use statistical tests to assess the significance of a model and of its parameters. Those tests are often performed automatically when fitting a model, so be mindful of $p$-hacking: you should decide on a significance level to reject or not the null hypothesis before looking at the test results, not after.

(2:uncertainty:test_params)=
### Statistical tests of the parameters

We can determine the significance of each parameter using a two-sided [$t$-test](2:hypothesistesting:ttest). The idea is to test if a parameter is significantly different from 0. This is mainly useful with the slope $\beta_1$, as it suggests that the predictor has a significant relationship with the outcome.

**Null and alternative hypotheses**

$H_0: \beta_1 = 0$

$H_A: \beta_1 \neq 0$

**Test statistic**

$$t = \frac{\hat{\beta}_1 - 0}{s_{\hat{\beta}_1}}$$

The same procedure can be used in multiple linear regression when interpreting the significance of each individual parameter. But when we have many predictors and we want to select only the significant ones, we might encounter an issue: as the number of tests increases, so does the probability of having at least one false positive. This probability is called the family-wise error rate. It means that while the significance level of each individual test stays the same, the global significance level of all the tests taken together does not. 

In that case, we need to apply a correction factor. Several methods exist, but the most common one is the Bonferroni correction: instead of performing each test at a significance level $\alpha$, we perform each individual test with a significance level of $\frac{\alpha}{c}$, where $c$ is the number of tests. If the tests are independent, then the global significance level of all the tests together will be $\alpha$.

### Statistical test of the model

On top of testing each coefficient individually, we can also test them all together, i.e., determine the significance of the whole model. For that we can use a two-sided [$F$-test](2:hypothesistesting:ftest), which compares the [deviation from the mean](2:regression:determination) (i.e., the variance) explained by the model and the deviation not explained by the model.

**Null and alternative hypotheses**

$H_0: \beta_0 = \ldots = \beta_m = 0$

$H_A: \beta_i \neq 0 \text{ for at least one }i$

**Test statistic**

$$
    F = \frac{\text{explained variance}}{\text{unexplained variance}} = \frac{ \frac{\sum_{i=1}^{n}(\hat{y}_i - \overline{y})^2}{\nu_\text{mod}} }{ \frac{\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}{\nu_\text{res}} }
$$

Where $\nu_\text{mod} = m$ and $\nu_\text{res} = n - m - 1$, $n$ is the number of data, and $m$ is the number of predictors.

### Statistical tests of the residuals

Here we mainly want to assess that the residuals $r$ meet the conditions to estimate confidence intervals and apply $t$-tests, i.e., that they are normally distributed. For that, we can use the Jarque-Bera test of normality, which tests whether the skewness and kurtosis match those of a normal distribution.

**Null and alternative hypotheses**

$H_0: \text{Skew}(r) = 0 \text{ and } \text{Kurt}(r) = 0$

$H_A: \text{Skew}(r) \neq 0 \text{ or } \text{Kurt}(r) \neq 0$

**Test statistic**

$$
    JB = \frac{n}{6}\left(\text{Skew}(r)^2 + \frac{\text{Kurt}(r)^2}{4}\right)
$$

Another test of normality that can be used is the omnibus $K^2$-test.

Other tests can also be used to check whether the model fulfills the [assumptions behind linear regression](2:regression:assumptions), for instance by testing whether the mean of the residuals is significantly different from 0, or by using the Durbin-Watson statistic. The Durbin-Watson statistic quantifies autocorrelation, i.e., whether patterns appears in the residuals, which should be just random noise. It lies between 0 and 4, and:
  * 2 means no autocorrelation.
  * $>$ 2 means negative autocorrelation.
  * $<$ 2 means positive autocorrelation.

You will learn more about autocorrelation in *Signals and Time Series*.
