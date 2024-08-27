# Overview

Bayesian inference is based on the Bayes' Rule which is a formula for updating our prior beliefs based on data.  It consists of four parts: *posterior, prior, likelihood,* and *marginal probability*.  ***posterior* =  (*prior* x *likelihood*) /  *marginal probability***.  

The ***prior*** is simply what is believed prior to seeing the data.  This could be subjective in nature, but it can also be backed by objective data based on prior experiments and research.

The ***likelihood*** is the probability of the data given the data.

The ***posterior*** is the result of multiplying the *prior* and the *likelihood*.  This *posterior* can then be used as the *prior* in the calculation of a new *posterior* backed by more data.

Since the ***marginal probability*** often involves advanced calculus (e.g. when the probability is a continuous variable) and may be extremely difficult, if not impossible, to calculate, simulation methods are often used to accurately approximate the true value of the posterior.

Using the **Beta Distribution**, here is a graphical representation of the learning process flow: ***prior* x *likelihood* ∝ *posterior***

-- INSERT BETA PROBABILITY DENSITY IMAGE --

# Comparison to Frequentist Statistics
  There are several  benefits of the Bayesian statistics over the more traditional frequentist approach:
  
  *Intuition*: Bayesian statistics lends itself to an approach that mimics a natural process of learning.  We begin with a belief (the *prior*).  That belief is confirmed or challenged with objective data (the *likelihood*), leaving us with a modified *posterior* belief.  The more data we have, the more accurate our belief.
  
  *Interpretation*: Bayesian inference results are also easier to interpret and communicate to stakeholders, especially in terms of the confidence. Confidence levels are often misinterpreted by stakeholders as the percentage certainty that the true mean or proportion lies between the confidence interval.  Frequentist confidence intervals in reality are a statement of confidence in the procedure rather than a direct probability statement of the model.  Bayesian credible intervals, on the other hand, do provide direct statements of probability of the data at hand and are, therefore, more intuitive.
  
  *Theory*: The frequentist methodology relies on the concept of the true parameter value which is the result of an infinite number of trials, a value which cannot be ever known with certainty.  The Bayes methodology establishes the probability based on a prior and the data at hand.  It considers the probability given the data as opposed to considering the data given the probability.\
  Secondly, the frequentist methodology is inherently biased towards the *null* hypothesis.  For example, if the p-value is above the determined threshold of .05, instead of "accepting" the *null* hypothesis, we "fail to reject" the *null* hypothesis.  This means that technically, we don't claim to know if the null is true; there just isn't enough evidence to say that it is not true.
  
  *Other*: In practice, if we compare frequentist A/B or MVT tests with a level of significance equal to .05 and 80% statistical power to the Bayesian methodology, the latter will reach a conclusion relatively faster.
  
  A common critique to the Bayesian methodology, however, is the inherent level of subjectivity in establishing a prior.


# Bayesian Inference with Example
### 1. Get Data
The data below is a prefabricated, but it serves as an example of the data required to run A/B testing.

-- INSERT DATAFRAME --

### 2. Define Prior
The *prior* reflects a belief about how we expect the different versions of the web page to perform.  We will quantify our prior belief using the **Beta Distribution**, which takes the form Beta(alpha,beta) or Beta(shape1,shape2).  In our case, *alpha* represents the number of visitors to the webpage that converted, and *beta* represents the number of visitors that did not convert.  The higher *alpha* and *beta*, the more data we have and thus, the stronger our prior belief.

In this example, we expect a 20% conversion rate for the control, so we will use Beta (2,8).  For the test version of the webpage, however, we expect a higher conversion rate, so we will use Beta (6,4).  In practice, the conversion rates for the two versions could use the same Beta Distribution, and likely would use Beta values that reflect only a slight change in conversion rate.

Note: A Beta(20,80) would also represent the same conversion rate for the control, but the density would be more concentrated around 20% and would imply a stronger held prior belief.  This, in turn, would more heavily influence the *posterior*.


-- INSERT BETA DISTRIBUTION OF PRIOR --

### 3. Define Likelihood
The *likelihood* can be derived from the A/B test data. Similar to our prior, the *alpha*/*shape1* will represent the conversions.  *beta*/*shape2* will represent non-conversions. There will be an *alpha* and *beta* for both the control and the test.\
\
Control *alpha*: 17489
Control *beta*: 127785
Test *alpha*: 17264
Test *beta*: 128047

-- INSERT BETA DISTRIBUTION OF LIKELIHOOD --


### 4. Calculate Posterior
After having established the priors and the likelihoods in the form of a Beta Distribution, we can now derive our posterior distribution. Essentially, we add the control and test prior *alphas* to the control and test likelihood *alphas* and the prior *betas* to both the corresponding likelihood *betas*.  Any overlap between the two distributions indicates uncertainty.

-- INSERT BETA POSTERIOR COMPARISON --

### 5. Simulation
We have calculated the posterior distributions of each variant.  To better understand the difference between the two distributions, we will run 1e6 simulations with random samples from each distribution.  Each sample will be selected based on its probability in the distribution.  This ensures that samples in regions with higher probability appear more frequently.

Then we will look at the quantiles and the 90% Credible Intervals of the simulated distributions.

-- INSERT QUANTILES --















