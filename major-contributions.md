## 1. Subset Analysis

Advocated for additional focus on Alzheimer's patients lacking the ApoE4 gene (more fine-grained analysis)

### Origin

Logistic regression, whole data

y=AD status, x= sAPPb-related variables(candidates) + control variables $\Rightarrow$ find significant sAPPb-related variables

### Problem

No significant variables; unclear guidance

Thought: Clarify the aim of the research

### Solution
After thorough discussions with medical collaborators, I found that the task could be divided into two parts:
- **Traditional/General**: Modeling on the whole data to identify variables which are likely associated with AD status
- **Specificed**: A particular subgroup of patients, who lack the ApoE4 gene—an important indicator associated with Alzheimer's Disease —yet still exhibit the disease, presents a significant area of interest. The pathogenic mechanism within this group is thought to be associated with the abnormally slow clearance rate of Ab42, suggesting a unique underlying pathology

Univariate regression: `sAPPb related variables ~ ApoE status`
$\Rightarrow$ Multiple testing correction $\Rightarrow$ Diagnostic: normal assumption


## 2. Cutoff Establishment
Established a cutoff to address the multiple testing problem

### Origin

Use logistic regression: AD status ~ sAPPb related variables + control variables to identify potential biomarkers (with respect to statistical significance)

### Problem

Too many possible model configurations (different combinations of candidates + combinations of control variables) $\Rightarrow$ Multiple testing problem

Not multiple hypothesis tests $\Rightarrow$ Traditional correction method e.g., Bonferroni, not applicable (If treat every variable's p-value in all multivariate regressions, it'll be too conservative to have any significant result)

### Solution

My reasoning is naive, grounded in basic statistical principles: 

Despite conducting numerous regressions (N=144), certain variables, such as the Fractional Clearance Rate (FCR) and Fractional Turnover Rate (FTR) ratios of sAPPb to sAPPa, have shown consistent significance across a multitude of models. 

This consistency suggests that their significance is unlikely to be mere coincidence, i.e., its significance in at least one model is not by chance. We aim to determine the minimum number of models—essentially, a cutoff—required to confidently assert that a variable's significance is not merely by chance.

Regarding hypothesis testing, significance by chance (where the null hypothesis is true yet still appears significant according to test statistics) occurs at a probability equal to the significance level, for example, 0.05 or 0.1. If we assume all tests are under the true null hypothesis, each test that shows significance can be considered a Bernoulli event with a probability equal to the significance level.

We are dealing with a scenario where we have conducted N independent tests. Each test has a probability $P(Y_i = 1) = p_0$ of being significant just by chance. We want to determine the minimum number of tests, n, that need to be significant to ensure that the observed significance is not just due to chance, under a specified error probabilitye (e.g., $e = 0.1$ or $e = 0.05$).

*In terms of the "consistency" I've mentioned, it should be $e=p_0=0.1$

The sum of significant tests: $$S=\sum_{i=1}^{N}Y_i$$, follows a binomial distribution $\text{Bin}(N = 144, p_0 = 0.1)$. We aim to find the cutoff $n$ such that the probability of having more than $n$ significant tests by chance is less than the error probability $e$. Mathematically, this is represented as:

$$P(S > n) = 1 - P(S \leq n) < e$$

Thus, we need to find n such that:

$$P(S \leq n) \geq 1 - e$$

In the context of a binomial distribution, this probability can be calculated as:

$$P(S \leq n) = F_S(n) = \sum_{i=1}^{n}\binom{144}{i} \times 0.1^i \times 0.9^{144-i}$$

We can set e for certain value and calculate **cutoff n** using qbinom(1-e, size, prob) in R.

*Details shown in ["Materials-multicollinearity-solution-cutoff.pdf"](Materials/multicollinearity-solution-cutoff.pdf)*

## 3. Both Explanatory and Predictive Modeling

### Origin

The "traditional/general task" mentioned before--identify biomarkers based on the whole dataset.

### Problem

What exactly is a "biomarker"? 

Is it through statistical significance or its predictive ability? Specifically, is it about its significant association with Alzheimer's Disease or its capacity to accurately predict AD?

### Solution

Firstly, we need to understand the [type of biomarker](https://www.atlasantibodies.com/knowledge-hub/blog/7-types-of-biomarkers/?language=en) we're discussing, which appears to be a diagnostic biomarker in this context.

Next, we must clarify our objective: are we aiming to explain or predict? In fact, the distinction between [explanation and prediction](https://www.stat.berkeley.edu/~aldous/157/Papers/shmueli.pdf) is a well-established and continuing debate in statistics.

Thus, I think integrating both approaches could be beneficial--if a variable demonstrates both statistical significance and predictive power, its reliability as a biomarker increases. By the way, our primary aim is not to explain or predict per se but to narrow down the list of candidates to a manageable number for further research.

Explanation can't be accurate since we have no idea what the true model of AD's underlying relationships is. However, a statistically significant association suggests potential biomarker qualities.

Similarly, a variable with high predictive power could indicate a relevant association with AD, suggesting its potential as a biomarker.

**Methods**:
- **Explanation**: Use multivariate logistic regression.
- **Prediction**: Employ shrinkage methods for variable selection, such as Lasso and Elastic Net.
  - Address multicollinearity, which can lead to unstable Lasso selections, by conducting a preliminary manual selection.
  - If control variables overshadow candidate variables, eliminating them from the selection process might be necessary. This allows us to focus on comparing sAPPb-related variables amongst themselves rather than with highly predictive control variables, including ApoE4 status.
