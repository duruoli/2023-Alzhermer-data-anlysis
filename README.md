# 2023-Alzhermer-data-anlysis

## Goal
Find potential sAPPbeta-related biomarkers for Alzheimer's Disease

## Outcomes

Three potential biomarkers:
- Fractional Turnover Rate (FTR) of sAPPb/ FTR of sAPPa
- Fractional Clearance Rate (FCR) of sAPPb/ FCR of sAPPa
- Delay times of sAPPb / Delay times of Ab40


## Contributions

1. Propose an extra focus on AD[+] subset. Novel findings on AD[+], i.e, AD patients subset

From focusing on whole data to focusing on subsets (or adding an extra focus), especially AD patients without ApoE4

-> dlt isn't significantly different across E4[+] and E4[-] in the whole data, but is different in AD[+] subset

- Thought: combine background knowledge

discuss with collaborators: from general solution (i.e., building explanatory or predictive models on the whole data, detecting significant variables or variables with high prediction power)

- Step: univariate regression -> multiple testing correction -> normal assumption diagnostic: U-test and T-test integrated

### 2. A novel method to solve multiple testing problem

Formulate a cut-off.

We are dealing with a scenario where we have conducted \( N = 144 \) independent tests. Each test has a probability \( P(Y_i = 1) = p_0 =0.1 \) of being significant just by chance. We want to determine the minimum number of tests, \( n \), that need to be significant to ensure that the observed significance is not just due to chance, under a specified error probability \( e \) (e.g., \( e = 0.1 \) or \( e = 0.05 \)).

*In terms of the "consistency" I've mentioned, it should be $e=p_0=0.1$

The sum of significant tests, \( S = \sum_{i=1}^{N} Y_i \), follows a binomial distribution \( \text{Bin}(N = 144, p_0 = 0.1) \). We aim to find the cutoff \( n \) such that the probability of having more than \( n \) significant tests by chance is less than the error probability \( e \). Mathematically, this is represented as:

$$P(S > n) = 1 - P(S \leq n) < e$$

Thus, we need to find \( n \) such that:

$$P(S \leq n) \geq 1 - e$$

In the context of a binomial distribution, this probability can be calculated as:

$$P(S \leq n) = F_S(n) = \sum_{i=1}^{n}\binom{144}{i} \times 0.1^i \times 0.9^{144-i}$$

We can set e for certain value and calculate n as the cutoff using qbinom(1-e, size, prob) in R.

### 3. Integration of explanatory power and predictive power

The final outcomes are consistent across these two perspectives: FTR, FCR are both statistically significant (being able to explain for variance of AD status) and with high predictive power

It's a critical question to ask: what does it mean to be potential biomarkers?

In terms of statistics, which perspective is our focus: explanatory or predictive?

The essence is to do variable selection, but for what? My answer is it's to prepare for future research.

Whether the variables are indeed contructive modulars in AD mechanism isn't the key, so predictive model can also be used, because strong predictor could be potentially related to the mechanism, though not necessarily directly related.

1) Significance:

- Problem 1: what is the model configuration?

Too many possible configurations -> integrate background knowledge (statistical preprocessing, i.e., multicollinearity & research interest)

- Problem 2: multiple testing

2) Prediction:

Lasso, Elastic Net

- Problem 1: multicollinearity -> lasso selection unstable -> solution: manually set subset of candidates (not put highly correlated variables in one candidate subset)
- Problem 2: control variables have too strong predictive power, causing no target variables are selected -> get rid of control variables (any potential problem?)

## Prospective topics (potential problems)

1. Two-step method (rather than parallel)

First ML predictive model to do initial filtering -> then losgitic regression

2. subset: normal testing first? than multiple testing regression

3. Statistical validation of the cut-off

4. Excluding control variables for variable selection is reasonable or not?


   
