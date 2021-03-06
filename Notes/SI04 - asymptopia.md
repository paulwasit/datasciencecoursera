
### Introduction

Asymptotics is the behavior of statistics as the sample size tends to INF.


### Law of large numbers (LLN)

The relative frequency of an event is the number of times an event occurs, divided by the total number of trials:

P(A) = ( Frequency of Event A ) / ( Number of Trials )

**Law of large numbers**, or **LLN**: 
The relative frequency of an event will converge towards its true probability 
as the number of trials increases.

An estimator is **consistent** if it converges to what you want to estimate.

+ the sample mean of iid samples is consistent for the population mean
+ the sample variance of iid samples is consistent for the population variance



### Central Limit Theorem (CLT)

> The sample mean distribution of iid variables
> will become normal, or nearly normal, as the sample size increases.

![\bar X \sim N~(\mu, \sigma^2 / n)](equations/normalCLT.png?raw=true)

Properly normalized, the distribution becomes a standard normal:

![\frac{\bar X_n - \mu}{\sigma / \sqrt{n}}~ \sim ~N(0, 1)~~when~n \gg 1](equations/CLT.png?raw=true)



### Confidence intervals (CI)

When we estimate something using statistics, usually that estimate comes 
with uncertainty. Take, for example, election polling. When we get a polled 
percentage of voters that favor a candidate, we were only able to sample a 
small subset of voters. Therefore, our estimate has uncertainty associated with it.

Confidence intervals are a convenient way to communicate that uncertainty in estimates.

The 2.5 and 97.5 percentiles are &plusmn;1.96 standard deviations from the mean (approx. &plusmn;2).

It means that:

![P (\bar X \in [\mu \pm 2\sigma / \sqrt{n}]) = 95\%](equations/normalCI.png?raw=true)

We can deduce from it the **95% interval for &#956;:**

![\bar X \pm 2\sigma / \sqrt{n}](equations/normalCI2.png?raw=true)

It means that for each value of the sample mean, the interval above has 95% chances to contain &#956;.

More generally, the &#913;th percentile Confidence Interval of an Estimate is:

![Est \pm ZQ \times SE_{Est}~~where~ZQ=Z_{ (1+\alpha)/2}](equations/CI.png?raw=true)


+ CI get narrower with less variability of the pop, and as the sample size increases
+ CI get wider as the confidence percentage decreases 

### Sample proportions

In a Bernoulli distribution with success probability p, the CI is:

![\hat p \pm z_{1 - \alpha/2}  \sqrt{\frac{p(1 - p)}{n}}](equations/bernoulliCI.png?raw=true)

We do not know p, but as p*(1-p) is minimal when p = 0.5, the largest 95% interval of p is given by:

![\hat p \pm \frac{1}{\sqrt{n}}](equations/bernoulliCI2.png?raw=true)

We can also use an exact binomail test:

```r
binom.test(sampleSuccessRate, sampleSize)$conf.int # returns the 95% CI for the binomial test
```

Or we can use p of our sample to approximate the 95% interval. This is called the Wald interval, and is works well 
when n is large.

_Note: adding 2 success and 2 failures, the Agresti/Coull interval, can give better results when n is too small: it brings p closer to 0.5, which gives the widest CI._


###Poisson interval

![poissonCI](equations/poissonCI.png?raw=true)

For a 95% CI, with x the number of events during a period t:

```r
lambda <- x/t 
round(lambda + c(-1, 1) * qnorm(0.975) * sqrt(lambda/t), 3)
```

We can also use an exact Poisson test:

```r
poisson.test(events, period)$conf # returns the 95% CI for the binomial test
```


